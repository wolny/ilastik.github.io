---
layout: documentation
title: Counting
tagline: Interactive Counting
category: "Documentation"
group: "workflow-documentation"
---
# Counting
## How it works, what it can and cannot do

Our counting approach is realized in a pixel-to-pixel regression algorithm to estimate the object density map of a given image, 
via which the object count in a region can be derived via summing over the aforementioned map.

The algorithm input are user given markers (see example below) in the form of dots (red)
for instances of the interesting object and brushstrokes for irrelevant background(green).
From these markers, the map is calculated and can be refined interactively by either placing more markers 
or manually fixing the number of objects in specific regions. 

While counting connected components via e.g. Pixel Classification is viable for very sparse data, 
overlapping objects in big clusters require our density-based regression algorithm.
Still, to provide accurate counts, similarity between individual instances is expected, most notably in size:
To ease the burden on the user, we focused on minimizing the amount of input that has to be provided, rather than manually labeling either the extent or the boundaries of a specific object, 
instead of marking the exact shapes of the objects, dots placed close to the centers are sufficient in our case.
![](counting_intro_overview.png)

![](counting_good_bad.png)

Complicated but separated objects with a high variability as seen on the left are more suited to the more general <a href = "../objectClassification"> Object Classification</a> module, on the other hand, clusters of small and overlapping instances as seen on the right are the focus of
our counting approach, dealing with these issues specifically.

## 1. Input Data
IMAGE OF IMPORT DIALOG HERE
The user can supply either images (e.g. *.png, *.jpg and *.tif) directly or pass hdf5 datasets.
Please note that the current version of the Counting module is limited to handling 2D data, as the performance is not satisfactory yet for larger volumes, for this reason hdf5-datasets with a z-axis are not accepted.
Only images requiring manual labeling, i.e. the training set have to be added in this way, the full prediction on the dataset can be done via Batch Processing.


## 2. Object size



The chosen Sigma should be large enough so that one gaussian-smoothed dot covers a single object.


## 3. Interactive refinement
Using LiveUpdate
Place Observerboxes
## Dots and stripes
Dots have to be placed close to the center
Cursor has the size of the currently selected Sigma

Most importantly dots on overlapping cells, otherwise training data incorrect.
Background: broad strokes, just marking unimportant stuff

Use boxes to get general idea of quality




## 4. Algorithm
### Random Regression Forest
2 different regressors are supplied in our framework.
Random Forest is fast and included in scikit-learn, which is a dependency for ilastik.
Requires more labels to give correct results over bigger dataset.
Good at handling background labels due to non-linearity




### Support Vector Machine
Requires Gurobi
Slower
Better generalization
Can offer additional type of label via Box constraints
-Box constraints not strict
#Box constraints
Box constraints offer an easy way to provide counts for a region, while not having to label every instance individually.




## Regression Parameters
We expose the most important and well-known parameters for our algorithms to the user, 
which consist of the following:
C: How much impact should individual and box errors do compared to w itself, this will likely only change results if you set C to low values.
epsilon: The amount of error that will be tolerated for individual pixels, this regularizes the result. 
though the defaults should already create good results.





## Exporting results
Possible to save the regressor
Will be loaded again, can do prediction directly if parameters and labels untouched
Can also save prediction itself
If you want to export the results for a single image, use exportLayerDialog.

[Batch prediction] ##Batch prediction
For large-scale prediction, first train regressor, then add input images, then press export all.



