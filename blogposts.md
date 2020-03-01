---
layout: default
title: Blog
navigation_weight: 2
---
# Blog Updates

| Description                                                                                                                | USCS symbol              | chorizon                      | Unsaturated | Saturated | Compacted | Saturated Compacted |
|----------------------------------------------------------------------------------------------------------------------------|--------------------------|-------------------------------|-------------|-----------|-----------|---------------------|
| Well graded   gravel, sandy gravel, with little or no fines                                                                | GW                       | sieveno4_r                    | 0           |           |           |                     |
| Poorly graded   gravel, sandy gravel, with little or no fines                                                              | GP                       | sieveno10_r                   | 0           |           |           |                     |
| Silty   gravels, silty sandy gravels                                                                                       | GM                       | sieveno40_r                   | 0           |           |           |                     |
| Clayey   gravels, clayey sandy gravels                                                                                     | GC                       | sieveno200_r                  | 20          |           |           |                     |
| Well graded   sands, gravelly sands, with little or no fines                                                               | SW                       | sandvc_r                      | 0           |           |           |                     |
| Poorly graded   sands, gravelly sands, with little or no fines                                                             | SP                       | sandco_r                      | 0           |           |           |                     |
| Silty sands                                                                                                                | SM                       | sandmed_r                     | 22          |           | 20        | 50                  |
| Loamy sand,   sandy clay Loam                                                                                              | SM-SC                    | sandfine_r                    | 7\*          | 10-20\*    | 50-75     | 14                  |
| Clayey sands                                                                                                               | SC                       | sandvf_r                      | 5           |           | 74        | 11                  |
| Inorganic   silts, silty or clayey fine sands, with slight plasticity                                                      | ML                       | siltco_r                      | 7           |           | 67        | 9                   |
| Inorganic   clays, silty clays, sandy clays of low plasticity                                                              | CL                       | claytotal_r                   | 4           |           | 86        | 13                  |
| Mixture if   inorganic silt and clay, moderately plastic                                                                   | ML-CL                    | avg of siltco and   claytotal | 6\*          | 10-20\*    | 65        | 22                  |
| Organic silts   and organic silty clays of low plasticity                                                                  | OL                       | om_r fraction of silt         | 5           |           |           |                     |
| Inorganic   silts of high plasticity                                                                                       | MH                       | siltfine_r                    | 20          |           | 10        | 72                  |
| Inorganic   clays of high plasticity                                                                                       | CH                       | claysizedcarb_r               | 25          |           | 103       | 11                  |
| Organic clays   of high plasticity                                                                                         | OH                       | om_r fraction of clay         | 10          |           |           |                     |
| Loam\*\*                                                                                                                     | ML, OL, MH, OH           |                               | 5-20\*       | 20-Oct    | 60-90     |                     |
| Silt Loam\*\*                                                                                                                | ML, OL, MH, OH           |                               | 5-20\*       | 20-Oct    | 60-90     |                     |
| Clay Loam,   Silty Clay Loam\*\*                                                                                             | ML, OL, CL, MH, OH,   CH |                               | 4-25\*       | 20-Oct    | 60-105    |                     |
| Silty clay,   clay                                                                                                         | OL, CL, OH, CH           |                               | 4-25\*       | 20-Oct    | 90-105    |                     |
| Peat and   other highly organic soils                                                                                      | Pt                       | om_r                          |             |           |           |                     |

NOTES:
\* Hyphenated classifications are "borderline" and incorporate plasticity aspects of both types depending on percentage
\*\* Loam is not classified in SSURGO metadata

## Update 2/17/20

### Landslide Density
We've explored a number of different methods for calculating the greatest density of landslide occurrences in the USA. Based on a point/polygon combined dataset of recorded landslide occurrences across the United States. The two methods we settled on were as follows:

The [Point to Raster](https://pro.arcgis.com/en/pro-app/tool-reference/conversion/point-to-raster.htm) tool allows a raster to be created from a point dataset. The tool works by creating a raster over the area containing the points. Each raster cell's value is computed using a combination of values from every point that lies within the cell. In our case, we simply had the raster store the number of points present in each cell. Each point in the dataset represents a landslide and all landslides were weighted equally.

The second potential method was to use a [fishnet](https://pro.arcgis.com/en/pro-app/tool-reference/data-management/how-create-fishnet-works.htm). Fishnets are essentially polygon layers that are shaped like rasters, the benefits of which include not having to make every cell a square, and the option to use polygon-to-polygon operations. In our case, fishnets were useful in conjunction with spatial joins. Joining the point layer and the fishnet layer gave us the number of points in any given cell, similar to the first method.

Both of these methods are flawed, due to issues inherent to the dataset. It's a combined dataset that was created from several state-level datasets. Some state datasets are more complete than others, some states have a greater or lesser threshold for what counts as a landslide and report landslides accordingly, and some states just have more robust data-collection programs than others. As a result, certain states have abnormally high or low amounts of landslides, which can skew the results.

Also, some states report landslides as polygons containing the affected area, while most use points. Our analyses disregarded polygons, but this could be handled with further calculations-- for example, we might convert each polygon into a single point by calculating the location each polygon's [centroid](https://en.wikipedia.org/wiki/Centroid) and replacing said polygon with a point at that centroid. 

Finally, not all landslides are the same-- some are of much greater magnitude than others-- but they were all treated equally in our study. Further research could lead to some method of weighting the various landslide occurrences so that larger landslides count for more than smaller ones.



### Python
Python is a versatile and flexible programming language that is relatively easy to learn and can be used in conjunction with ArcGIS and QGIS. In this class, we will be using it for geoprocessing operations.

The basic concepts of a programming language are pretty simple! A program is a set of instructions that a computer will carry out. Due to the nature of Newtonian physics, a computer will always follow the instructions in the same way every time, meaning the results you get are always going to be deterministic. You'll only get something different out if you put something different in. 

Python's instructions are easy to understand. `a=0` finds a space in the computer's memory, calls it `a`, remembers where to find it, and sets the memory's value to 0 at that location. In fewer words, it creates a variable named `a` and sets it to 0. But, each Python instruction is translated into language that is easier for machines to read-- sequences of zeroes and ones that the computer understands mean to move things between the RAM and different parts of the CPU. But that's really quite hard to understand, so Python wraps those instructions into a more human-readable format, known as a high-level programming language.

Just like how Python's commands are a bunch of computer-level commands wrapped up nicely in human-readable format, we can save important sets of instructions and repeat them without having to write every instruction out over and over again. The keyword `def` allows for creation of a function. A function is a set of instructions for Python to run. Functions can have inputs and outputs, but they don't necessarily need to. Here is an example of a function without inputs or outputs.
```
def a():
  print ("hello world!")
```
In this case, `a()` is just a shorter way to say `print("hello world!")`. We can also have functions that take inputs.
```
def b(number):
  print (number + 5)
```
This prints whatever number is between the parentheses, plus 5. For example, `b(5)` prints 10.

Python gives users the option of object-oriented programming, which is useful in creating a program with many different components that have their own attributes and can do things on their own inherent to themselves. Object-oriented programming is vital for GIS applications and will be covered in a future blog post.

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
