scNOVA methods > single cell data
upgrade - how to incorporate information of copy number information

upgrade - consider high-ploidy/complex rearranged cells.

Google drive & github page > exchange scripts and input data

Alvaro > copy number status for cell line for training (RPE-1 C7, BM5-10)
incorporate CN status as additional layer to the input feature matrix (150 bins for each genes)
similar number of cells > pseudobulk

Technical issues/discussion points
Q)which one would be more accurate among 200kb bins and supersegment?
A) Supersegment > segmentation/merging of supersegments - less noisy

Q) For C7, which has complicated region in ch10, there is BFB cycle and highly amplified region > do we need manual correction?
A) we only have rough estimates (~100 copies), but not exact copy number value. We don't know how much this would affect the model. Would this be problematic? A (Hyo): We don't need precise number but we do need the range for each segment. Are there numbers or is it unpredictable? A(Alv): there are some numbers (5), but it's hard to know the exact value, let alone the range. Any ideas? A) High copy numbers are something people want to tackle, so it won't be a good starting point for training. Should start with slight derivations.

graph: 
x: total read count, normalized
y: watson fraction
outlier: copy number of 400+, other cells with 100+
> Solution) exclude the outlier region for training
> Or give it a categorical value rather than a continuous one (for what tho)

Train using data with copy number up to 4, 5 is risky due to outliers. Maybe try blacklisting CN 5 first then if it works well move on to 5.

Train the model without relying on the labels but rather the binned version of the histograms

from the CN map > flatmap it to 10x10 bin table and feed it to the model (idk check on this later)


take median of cells
- pseudobulk level training - take median of several cells
Assumption: most region has clonal number status

In the case where we seperate the subclone - in making pseudobulk step - take subclones separately > not expect much difference in CN.

Try out CN as input OR use bin raw read count OR bin normalized read count
First layer (NO) is based on normalized read depth > Maybe a bit redundant?
Adding Watson fraction of the bin, that would be enough to infer the copy number. Wf is in the supersegment file.

CN status + Wf from supersegment as layers - completed this week probably


Q) Further cell line for CN calculation
LCL cells, which was already used for secondary evaulation in the original scNOVA

**Task for me** - use continuous value for label instead of binary.
first use pseudobulk - dynamically change pseudobulk sizes (downsampling evaluation)


----
In the shared google drive folder - excel table compiling all possible data sets, path, etc.


---
RECAP
Alvaro - LPL data, RNA-seq analysis
Hyo - try out different input types
add CN layer (supersegment) and possibly WC > evaluation











