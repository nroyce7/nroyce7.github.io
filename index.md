# Projects

These are some of the projects I am working on or have completed!

## Optical Vortices

I worked on a proof of concept system that uses the optical phenomenon known as an Optical Vortex created with a spatial light modulator, paired with programmable Arduino Boards to encode and decode the beam in order to transmit data through air. <br />
[Read More](https://github.com/nroyce7/nroyce7.github.io/blob/master/Optical%20Vortices.md)

<br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/Helix_oam.png?raw=true" width="200" class="center">

## Surface Plasmon Resonance

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
I knew that the filaments in a lightbulb were coils but until I saw it in an SEM I had no idea it was a coil of coils. <br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/filament%20sem.jpg?raw=true" width="500">

### Wood Fiber (SEM)
I really love this image but I'm not a biologist so I have no idea what I'm looking at.<br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/wood%20sem.jpg?raw=true" width="500">

### Mushroom Gill (SEM)
This is the higest magnification picture I've taken with the SEM and once again I'm not entirely sure what I'm looking at but I think it might be the spores of the mushroom.<br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/mushroom%20sem.jpg?raw=true" width="500">

### Copper Wire (Optical)
This was a small piece of copper wire I found in the lab at 400x magnification, where you can see the slight gouges from the wire-drawing process that made it.<br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/400x%20copper%20wire.jpg?raw=true" width="500">

### Leaf (Optical)
Here's another example of my limited knowledge of biology, but here is a leaf at 400x magnification. I don't know what kind of leaf it is but I do know we are looking at the plant cells.<br />
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/40x_flowerPetal.jpg?raw=true" width="500">




