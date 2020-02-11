---
layout: default
title: Blog
navigation_weight: 2
---
# Blog Updates
## Update 2/10/20
We are calculating landslide risk according to a model put forth by Iverson et al. 2000.
This model states the following: 
#### Stress Factor = Resistance Factor / Driving Factor = (tan φ) / (tan θ) + [C - ψt * γw * (tan φ)] / [γr * H * (sin θ) * (cos θ)]
Basically, the resistance factor is the soil's resistance to shear and the driving factor is the forces that will cause the soil to shear. Let's break that down a bit.

- φ is internal angle of friction in degrees. This is determined by laboratory testing of different soil types and consistencies, and tells at at what angle the soil will shear.
- θ is hillslope in degrees. Hillslope determines the amount of shear stress and resisting forces.
- C is soil cohesion (Pa = kg/m/s^2) which varies depending on the type of soil. For example, silty or clayey soils are more cohesive than gravelly soils.
- ψt is pressure head (m); h/cosθ which is the height of the water table.
- γw is unit weight of water (N/m^3); N=kg*m/s^2 which is a constant for our purposes.
- γr is unit weight of soil regolith (N/m^3), which can be determined by finding the soil bulk density in kg/m^3 and multiplying by the acceleration due to gravity to find the weight.
- H is soil regolith thickness (m), which can be found by the depth to bedrock.
