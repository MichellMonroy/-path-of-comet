# Path-of-comet
Simulation of path of an especific comet in C and MPI

## Introduction
Generally speaking, a comet is a celestial body composed mainly of solid matter like ice with organic resting material, dust and rocks. They can have elliptical, parabolic, or hyperbolic orbits, but the most common in the solar system are the elliptical orbits.

The study of the trajectories of a comet date back to the 16th century, when Edmund Halley tried to calculate the trajectory of the comet that would later carry his lastname, using Newton's theory of gravitation as support. In this experiment he discovered that this orbit had a periodic behavior of 76, 77 years.
Later in 1821, the German mathematician Johann Encke discovered another comet whose orbit was also periodic, with a period of 3.3 years

I will focus on calculating the path of a specific comet, in this case, Halley Comet which is considered a young comet (P-AGE < 30) and dwarf comet < 1.5 km of diameter.
The coordinate system will have the sun at the origin, that means, heliocentric coordinates will be used to calculate the orbit.
As an ephemeris for this comet I will use the following date 03/15/1998.

Ephemeries are available on [Horizons](https://ssd.jpl.nasa.gov/horizons.cgi)

## Objetive
- Simulate the orbit of Halley's Comet
- Then simulate the trajectory of the planets of the solar system.


## Methodology
The project consists of the following files:
- element: Here are the functions of the population's elements (in this case the bodies of the solar system).
- integrator: This file calculates the speed and position of each element according to time.
- population: Contains the functions that can be applied to a set of elements, such as creating a new population, add new elements, and print the elements of that population.
- recipes: This file calculates the distance between the elements of a population.
- main: It is in charge of gathering the previous files so if we given a population and certain conditions initial like input, the position (x, y, z) and speed (vx, vy, vz) can be calculated according to time. This file uses MPI to optimally perform the calculations of each element in a population regardless of size, therefore it is necessary to have MPI installed to run the file.
- view3D.py: It's a program written in Python 3.7 which takes the results obtained in main.c and graphs the position of each element in the population. 
The number of graphs depends on the number of iterations that are indicate in the line 66 of main.c.


To run main.c it is necessary to download the full git and follow these steps:

1. Run the GNUmakefile file with the following command *make* .
2. Execute main with the following command *mpiexec -n 'number of processes to use' ./main > output.dat*. In this case I used 24 processes to speed up the calculation.
3. The previous command returns a file called **output.dat** if you change the name of that file, you must put the same name on line 14 of view3D.py in addition to creating a folder called "data" to save the graphs.
4. If you want to make a video with the graphs to see the change between them, you can enter [Gifmaker](https://gifmaker.me/).


## Initial Conditions 
The chosen date is march 15th 1998.
Using that date, we have the following information:
| Name | Mass | X | Y | Z | VX | VY | VZ |
| -- | -- | -- | -- | -- | -- | -- | -- |
| Sun | 1.989e+30 | 0 | 0 | 0 | 0 | 0 | 0 |
| Jupiter | 1.898e+27 | 4.581e+00 | -2.008e+00 | -9.428e-02 | 2.931e-03 | 7.271e-03 | -9.574e-05 |
| Saturn | 5.683e+26 | 8.636e+00 | 3.550e+00 | -4.051e-01 | -2.415e-03 | 5.156e-03 | 6.478e-06 |
| Neptune | 1.024e+26 | 1.507e+01 | -2.610e+01 | 1.899e-01 | 2.700e-03 | 1.595e-03 | -9.478e-05 |
| Uranus | 8.681e+25 | 1.255e+01 | -1.537e+01 | -2.199e-01 | 3.020e-03 | 2.312e-03 | -3.070e-05 |
| Earth | 5.972e+24 | -9.892e-01 | 9.993e-02 | -4.685e-07 | -2.010e-03 | -1.717e-02 | -6.054e-07 |
| Venus | 4.867e2+4 | -6.287e-01 | -3.540e-01 | 3.145e-02 | 9.783e-03 | -1.771e-02 | -8.067e-04 |
| Mars |  6.39e+23 | 1.345e+00 | 4.282e-01 | -2.409e-02 | 3.706e-03 | 1.452e-02 | 3.954e-04 |
| Mercury | 3.285e+23 | 3.430e-02 | 3.051e-01 | 2.177e-02 | -3.360e-02 | 4.179e-03   3.425e-03 |
| Haley | 2.2e14 | -3.135e+00 | 9.551e-01 | 1.833e-01 | -1.373e-03 | -9.206e-03 | 1.379e-04 |

Is necessary to use Astronomical Unit (au) as metric in X, Y & Z and au/day in VX, VY & VZ where:
- au = 149,597,870.7 km
- day = 86400.0 seconds

## Results
The result is in *output.dat* file generated when running main. In the following links there is a video in which you can see the results of 2 simulations different.

[Sun and Halley](https://drive.google.com/file/d/1-8b9hEDP-P7key8j2RUkyfi60CnNfXz8/view?usp=sharing)

[Solar system and Halley](https://drive.google.com/file/d/1sMrY7uikySPxscVMTttsb_Zr8TpHq27y/view?usp=sharing)

[Solar system and Halley (scale)](https://drive.google.com/file/d/19i0Mjx8frIiA_XL1GTe7e5PMzH8Gi7KE/view?usp=sharing)

