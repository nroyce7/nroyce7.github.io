# Projects

These are some of the projects I am working on or have completed!

## Data Transmission With Optical Vortices
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/research.JPG?raw=true" width="1000">

## Surface Plasmon Resonance

![\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}](https://latex.codecogs.com/svg.latex?x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D)

<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/spr%20setup.jpg?raw=true" width="300">
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/afm.jpg?raw=true" width="500">

## Fiber Characterization
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/Noah%20Royce%20NANO-230-page-001.jpg?raw=true" width="1000">

## Simulations
Kinematics with variable mass
```python
import matplotlib.pyplot as plt

g = -9.8 #m/s^2
dt = 1

thrust = 210
dm = -1 #kg/s
fuselage_mass = 10
vel = 0
pos = 0

acc_plt = []
vel_plt = []
pos_plt = []

for t in range(25):
    fuel_mass = 10 + (dm*t)
    if fuel_mass <= 0:
        fuel_mass = 0
        thrust = 0
    rocket_mass = fuel_mass + fuselage_mass

    acc = thrust/rocket_mass + g
    vel = vel + acc*dt
    pos = pos + vel*dt
    
    if pos < 0:
        pos = 0
    
    acc_plt.append(acc)
    vel_plt.append(vel)
    pos_plt.append(pos)

plt.plot(acc_plt)
plt.plot(vel_plt)
plt.plot(pos_plt)
```

## Microscopy
These are images I've taken with various microscopes at UW Stout.

### Tungsten Filament (SEM)

<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/filament%20sem.jpg?raw=true" width="500">

### Wood Fiber (SEM)

<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/wood%20sem.jpg?raw=true" width="500">

### Mushroom Gill (SEM)

<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/mushroom%20sem.jpg?raw=true" width="500">








