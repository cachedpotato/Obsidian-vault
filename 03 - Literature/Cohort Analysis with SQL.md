---
tags:
---
# Cohort Analysis with SQL
Cohort Analysis is a type of analysis where we divide users/customers into distinct cohorts and measure the retention rate. Often times cohorts are divided by time period, and this period can vary from field to field. For example, if we were to perform cohort analysis on a live-service game, we may want our cohorts to be separated by day, whereas for tourist data, we may want the time period to be a lot longer such as 3~6 months.

The output of cohort analysis would look something like this after pivoting:
![[bzbog3i3.bmp]]
We can see the retention rate of different cohort groups over user lifetime. In other words, we can see the overall trend of user dropouts over time. Column wise, we can see the retention rate over product life cycle. That is, we can see how well our product in general is doing over time. If we see a steep downward trend column wise, this means the product is not doing as well as it did before.

## SQL Code

### Key Functions
There are 2 very important date functions that we'll be seeing a lot of:
- `DATE_DIFF`: for getting cohort indexes
- `DATE_TRUNC`: for grouping users into cohorts

### Step 1. Getting Initial Date
Now that we have the basics out of the way, let's get started with the code. The very first thing we need to do is to split user into different cohorts. For this, we need:
- User data (user ID)
- Initial Purchase/Login/... Date 
```SQL
SELECT
	user_id
	DATE(MIN(purchase_date)) AS cohort_day --initial purchase date = cohort index
FROM
	sales_data
GROUP BY
	user_id;
```

### Step 2. Appending cohort day data
Next, we need to [[SQL Join Operations|join]] This with our sales data, so that we get both
- initial purchase date (cohort group)
- invoice(purchase/login/..) date (cohort index)
```SQL
WITH initial_purchase AS (
	SELECT
		user_id,
		DATE(MIN(purchase_date)) AS cohort_day
	FROM
		sales_data
	GROUP BY
		user_id
)
SELECT
	s.*,
	i.cohort_day
FROM
	sales_data s JOIN initial_purchase i ON s.user_id = i.user_id;
```

### Step 3. Getting Cohort Index (columns)
Here starts the hard part. To get the rows as the table above, we need to get the number of users within each cohort that made an invoice in that particular cohort index. In this example, the time interval is 1 month.
```SQL
WITH initial_purchase AS (
	SELECT
		user_id,
		DATE(MIN(purchase_date)) AS cohort_day
	FROM
		sales_data
	GROUP BY 
		user_id
)
SELECT
	s.*,
	i.cohort_day,
	DATE_DIFF(DATE(s.purchase_date), i.cohort_day, MONTH) as cohort_index
FROM
	sales_data s JOIN initial_purchase i ON s.user_id = i.user_id;
```

### Step 4. Getting Cohort Groups (rows)
We're almost done! One of the last things we need to do is to put users into cohort groups. Currently we only have the columns (cohort indexes) sorted out, but now we need to group users into cohorts. This will be done using the `cohort_day` value. As mentioned, in this example the cohort's time interval is one month, so cohort groups do something like:
- 2020/01/01: Cohort group 1
- 2020/02/01: Cohort group 2
- 2020/03/01: Cohort group 3 ...
``` SQL
WITH initial_purchase AS (
	SELECT
		user_id,
		DATE(MIN(purchase_date)) AS cohort_day
	FROM
		sales_data
	GROUP BY
		user_id
)
SELECT
	s.*,
	DATE_DIFF(DATE(s.purchase_date) - i.cohort_day) AS cohort_index,
	DATE_TRUNC(DATE(i.cohort_day), MONTH) AS cohort_group
FROM
	sales_data s JOIN initial_purchase i ON s.user_id = i.user_id;
```
The `DATE_TRUNC()` function will truncate the date into the same day/month/year depending on the second parameter, which in this case was month. In essence, anything with a date value within the same month will have the same `DATE_TRUNC(, MONTH)` value of `year/month/01`

### Step 5. Getting User Count data
We're at the final stretch. We have both row and columns set up, all we need now is the actual user count data.
```SQL
WITH initial_sales AS (
	SELECT
		user_id,
		DATE(MIN(purchase_date)) AS cohort_day
	FROM
		sales_data
	GROUP BY
		user_id
)
SELECT
	COUNT(DISTINCT user_id) AS user_count, --actual data
	cohort_group, -- row
	cohort_index -- column
FROM (
	SELECT
		s.*,
		DATE_DIFF(DATE(s.purchase_date), i.cohort_day, MONTH) AS cohort_index,
		DATE_TRUNC(DATE(i.cohort_day), MONTH) AS cohort_group
	FROM
		sales_data s JOIN initial_purchase i ON s.user_id = i.user_id
) AS cohort_info
GROUP BY
	cohort_group,
	cohort_index
ORDER BY
	cohort_group ASC;
```

### Step 6. un-flattening of the table
Currently, our table will have the columns
- user count
- cohort index
- cohort group
To get the graph above, we need to unflatten this table in such a way that the `cohort_index` becomes the columns. We can achieve this _OUTISDE OF SQL_ with pretty much any tool that supports _pivoting_

## Time Series Graph
Using the pivot table created in Step 6, we can now create a time series graph to visualize everything:
![[d0yowirz.bmp]]
We can see instantly which cohorts have the most "loyal" users and which cohorts have the highest drop-outs (churning rate). 


---
Categories: [[050-Statistics]], [[SQL]]
References:
https://medium.com/@hafesafghan/cohort-analysis-in-sql-retention-rate-vs-churn-rate-ae951a28c7d4
https://ssongblog.tistory.com/35
