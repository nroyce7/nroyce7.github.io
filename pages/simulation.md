## Simulations

### Concentric Circular Orbits
```python
import math
import pygame as pygame

pygame.init()
screen = pygame.display.set_mode([700, 700])
surf = pygame.surface.Surface([700, 700])
surf.fill((255,255,255))
surf.set_colorkey((255,255,255))
running = True

screen.fill((255, 255, 255))

offset = 350
phase_shift = 0
r1 = 300.0
r2 = 100
t = 0.0
pos = []
lines = []



while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    screen.fill((255, 255, 255))
    orbit1 = pygame.draw.circle(screen, (0, 0, 0), (offset, offset), r1, 2)
    orbit2 = pygame.draw.circle(screen, (0, 0, 0), (offset, offset), r2, 2)
    planet1 = pygame.draw.circle(screen, (0, 0, 0), pygame.math.Vector2(r1 * math.cos(t) + offset, r1 * math.sin(t) + offset), 8)
    planet2 = pygame.draw.circle(screen, (0, 0, 0), pygame.math.Vector2(r2 * math.cos(2*t + phase_shift) + offset, r2 * math.sin(2*t + phase_shift) + offset), 8)
    if round(t, 2).is_integer():
        pygame.draw.line(surf, (0, 0, 0), pygame.math.Vector2(r1 * math.cos(t) + offset, r1 * math.sin(t) + offset),
                     pygame.math.Vector2(r2 * math.cos(2*t + phase_shift) + offset, r2 * math.sin(2*t + phase_shift) + offset))
    screen.blit(surf, (0, 0))
    print(t)
    t += 0.01
    pygame.display.flip()

pygame.quit()
```
<video src="/videos/ps_0_1.mp4" width="420" height="300" controls preload></video>
<\br>
<\br>

### Simple Rocket with Variable Mass
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

### Pi Day Collisions

