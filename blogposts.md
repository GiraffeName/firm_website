---
layout: default
title: Blog
navigation_weight: 2
---
# Blog Updates

## Update 2/17/20

### Landslide Density
We've explored a number of different methods for calculating the greatest density of landslide occurrences in the USA. Based on a point/polygon combined dataset of recorded landslide occurrences across the United States. The two methods we settled on were as follows:

The [Point to Raster](https://pro.arcgis.com/en/pro-app/tool-reference/conversion/point-to-raster.htm) tool allows a raster to be created from a point dataset. The tool works by creating a raster over the area containing the points. Each raster cell's value is computed using a combination of values from every point that lies within the cell. In our case, we simply had the raster store the number of points present in each cell. Each point in the dataset represents a landslide and all landslides were weighted equally.

The second potential method was to use a [fishnet](https://pro.arcgis.com/en/pro-app/tool-reference/data-management/how-create-fishnet-works.htm). Fishnets are essentially polygon layers that are shaped like rasters, the benefits of which include not having to make every cell a square, and the option to use polygon-to-polygon operations. In our case, fishnets were useful in conjunction with spatial joins. Joining the point layer and the fishnet layer gave us the number of points in any given cell, similar to the first method.

Both of these methods are flawed, due to issues inherent to the dataset. It's a combined dataset that was created from several state-level datasets. Some state datasets are more complete than others, some states have a greater or lesser threshold for what counts as a landslide and report landslides accordingly, and some states just have more robust data-collection programs than others. As a result, certain states have abnormally high or low amounts of landslides, which can skew the results.

Also, some states report landslides as polygons containing the affected area, while most use points. Our analyses disregarded polygons, but this could be handled with further calculations-- for example, we might convert each polygon into a single point by calculating the location each polygon's [centroid](https://en.wikipedia.org/wiki/Centroid) and replacing said polygon with a point at that centroid. 

Finally, not all landslides are the same-- some are of much greater magnitude than others-- but they were all treated equally in our study. Further research could lead to some method of weighting the various landslide occurrences so that larger landslides count for more than smaller ones.


## Update 2/10/20
Landslides are a combined problem of Newtonian physics and material properties. Different soils behave in predictable manners according to their textures, moisture content, and internal stresses. Knowing how soils behave under certain conditions will allow us to predict the risk of landslides for an area given data about that area. 
We are calculating landslide risk according to a model put forth by [Iverson et al. 2000](https://doi.org/10.1029/2000WR900090).
This model states the following: 
#### Stress Factors = Resistance Factors / Driving Factors
or
#### Stress Factors = (tan φ) / (tan θ) + [C - ψt * γw * (tan φ)] / [γr * H * (sin θ) * (cos θ)]
Basically, the resistance factor is the soil's resistance to shear and the driving factor is the forces that will cause the soil to shear. Let's break that down a bit.

- φ is internal angle of friction in degrees. This is determined by laboratory testing of different soil types and consistencies, and tells at at what angle the soil will shear. [This site](http://www.geotechdata.info/parameter/cohesion.html) is an example of these tested values.
- θ is hillslope in degrees. Hillslope determines the amount of shear stress and resisting forces, and we can get the data from a digital elevation model (DEM) that has been processed to calculate slope or relief.
- C is soil cohesion (Pa = kg/m/s^2) which varies depending on the type of soil. For example, silty or clayey soils are more cohesive than gravelly soils.
- ψt is pressure head (m); h/cosθ which is the height of the water table.
- γw is unit weight of water (N/m^3); N=kg*m/s^2 which is a constant for our purposes.
- γr is unit weight of soil regolith (N/m^3), which can be determined by finding the soil bulk density in kg/m^3 and multiplying by the acceleration due to gravity to find the weight.
- H is soil regolith thickness (m), which can be found by the depth to bedrock.

With the right data sets and unit conversions, we'll be well on our way.
