---
tags:
---
# Updating State List and State Objects in React
Basics are covered [[React Hooks|here]], but This got confusing for me so I'm just gonna create a separate note.

## Updating State List
For adding, we use the spread `...` operation, and for removing we're going to use `filter`
```jsx
function MyComponent() {
	const [foods, setFoods] = useState([]);

	function addFood() {
		const food = document.getElementById("foodInput").value;
		document.getElementById("foodInput").value = "";
		setFoods((f) => [...f, food]);
	}

	function removeFood(index) {
		setFood(f => f.filter(_, idx) => idx !== index);
	}

	return(
		<>
			<h1>Foods List</h1>
			<ul>
				{foods.map((food, index) => <li 
					key={index}
					onClick ={() => removeFood(index)}>
					{food}
				</li>)}
			</ul>
			<hr />
			<input type="text" id="foodInput" placeholder="Enter Food" />
			<button onClick={addFood}>Add Food</button>
		</>
	)
}
```

## Updating State Objects
```jsx
function MyComponent() {
	const [car, setCar] = useState({
		year: 2024,
		make: 'Ford',
		model: 'Mustang'
	});

	function handleYearChange(event) {
		setCar((c) =>
		({...c, year: event.target.value})
		);
	}

	return(
		<div>
			<input type="text" value={car.year} onChange={handleYearChange} />
		</div>
	)
}
```

---
Categories: [[React]], [[React Updater Functions]]
References:
