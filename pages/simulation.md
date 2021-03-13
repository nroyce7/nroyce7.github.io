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
<br />
<br />

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
```python
import pygame

class Square:
    def __init__(self, posx, mass, vel, length):
        self.posx = posx
        self.mass = mass
        self.vel = vel
        self.length = length

pygame.init()
width = 700
height = 500
screen = pygame.display.set_mode((width, height))
done = False
myfont = pygame.font.SysFont("3ds", 100)

digits = 0
plane_y = 300
RED = (255,0,0)
dt = 1/1000

s1 = Square(100, 1, 0, 25)
s2 = Square(200, 100**(digits), -0.01/dt, 150)

collisions = 0

def collide():
    new_vel1 = (((s1.mass - s2.mass)/(s1.mass + s2.mass))*s1.vel) + (((2*s2.mass)/(s1.mass + s2.mass))*s2.vel)
    new_vel2 = (((2*s1.mass)/(s1.mass + s2.mass))*s1.vel) + (((s2.mass - s1.mass)/(s1.mass + s2.mass))*s2.vel)

    s1.vel = new_vel1
    s2.vel = new_vel2


def hit_wall():
    s1.vel *= -1


while not done:
        for event in pygame.event.get():
                if event.type == pygame.QUIT:
                        done = True

        for i in range(100):
            print(collisions)
            s1.posx += s1.vel*dt
            s2.posx += s2.vel*dt

            if(s1.posx + (s1.length) < s2.posx or s1.posx > s2.posx + (s2.length)):
                pass
            else:
                collide()
                collisions += 1

            if(s1.posx <= 0):
                hit_wall()
                collisions += 1

            screen.fill((0, 0, 0))
            box1 = pygame.draw.rect(screen, RED, (s1.posx, plane_y, s1.length, s1.length))
            box2 = pygame.draw.rect(screen, RED, (s2.posx, plane_y-125, s2.length, s2.length))
            ground = pygame.draw.rect(screen, (255,255,255), (0, 326, 1080, 1000))
            count = myfont.render(str(collisions), 1,(0,0,0))
            screen.blit(count, (10,320))
        pygame.display.flip()
```
<video src="/videos/PiDay.mp4" width="420" height="300" controls preload></video>

### Mechanical Wave

```
import math
import pygame as pygame

pygame.init()
screen = pygame.display.set_mode([1080, 720])
surf = pygame.surface.Surface([700, 500])
surf.fill((255, 255, 255))
surf.set_colorkey((255, 255, 255))
running = True

screen.fill((255, 255, 255))

offset_x = -25.0
offset_y = 200.0
column = 25
row = 11
n = 50
r1 = 30.0
t = 0.0
dt = 0.005
pos = []
lines = []
balls = []

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    screen.fill((255, 255, 255))

    for i in range(0, column):
        pos.append(pygame.math.Vector2(r1 * math.cos(t + i*n) + offset_x + i*n, r1 * math.sin(t + i*n) + offset_y))

        for j in range(0, row):
            balls.append(pygame.draw.circle(screen, (0, 0, 0), pygame.math.Vector2((1 - j*0.1)*r1 * math.cos(t + i*n) + offset_x + i*n,
                                                                                   (1 - j*0.1)*r1 * math.sin(t + i*n) + offset_y + j*n), 5))

    for i in range(0, column-1):
        lines.append(pygame.draw.line(screen, (0, 0, 0), pos[i], pos[i + 1]))

    pos = []
    balls = []
    lines = []

    screen.blit(surf, (0, 0))
    print(t)
    t += dt
    pygame.display.flip()
```
<video src="/videos/wave.mp4" width="420" height="300" controls preload></video>
