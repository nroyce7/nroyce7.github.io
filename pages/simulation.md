## Simulations

### Ising Model

```
import pygame
from random import randrange, random
import numpy as np

# Initial size
I = 800  # must be even
J = 800  # must be even
size = 1
X = I * size
Y = J * size
N = I * J

# Pygame window
# *** Modify pygame.display.set_mode() to add bottom margin for numerical display
pygame.init()
window = pygame.display.set_mode((X, Y + 120))
clock = pygame.time.Clock()
colors = [(255, 0, 0), (255, 255, 255), (0, 0, 0)]  # red (0, never used), white (1), black (-1)
font = pygame.font.SysFont("freesansbold.ttf", 40)


ntries = 2000  # How many spin updates per screen update

# Initial parameters
T = 0  # temperature
H = 0  # external magnetic field

# Initial random state
M = 0  # target initial magnetization: 0 = random, -1 = all black, 1 = all white
spin = np.zeros((I, J), int)
for i in range(I):
    for j in range(J):
        spin[i, j] = 1 if M + (2 * random() - 1) > 0 else -1


# Interaction Energy for a particle
def inter_energy(i, j):
    return 2 * spin[i, j] * (spin[i-1, j] + spin[i, j-1])


# Total System Energy
def total_energy(I, J):
    inter_sum = 0

    for i in range(I):
        for j in range(J):
            # *** Calculate initial energy
            inter_sum += inter_energy(i, j)
    return -(H*np.sum(spin))-inter_sum


# Draw the initial state
for i in range(I):
    for j in range(J):
        pygame.draw.rect(window, colors[spin[i, j]], (i * size, j * size, size, size))
        # *** Calculate initial energy

E = total_energy(I, J)
# Simulation loop
fps = 60
run = True

while run:
    # Event loop
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    pygame.draw.rect(window, colors[-1], [[0, 800], [800, 920]])

    # Monte Carlo moves
    for n in range(ntries):
        # Randomly choose a spin to flip
        rand_i = randrange(I)
        rand_j = randrange(J)

        # *** Compute the change in energy if flipped
        spin[rand_i, rand_j] = spin[rand_i, rand_j] * -1
        field = spin[rand_i-1, rand_j] + spin[(rand_i+1)%I, rand_j] + spin[rand_i, rand_j-1] + spin[rand_i, (rand_j+1)%J] + H

        E_delta = -2*field*spin[rand_i, rand_j]

        # *** Accept or reject move base on Metropolis rule
        # if :
        # *** flip spin in numpy array
        # *** update total energy
        # *** update the spin graphically in the window
        if E_delta <= 0:
            E += E_delta
            pygame.draw.rect(window, colors[spin[rand_i, rand_j]], (rand_i * size, rand_j * size, size, size))
        else:
            r = np.random.uniform()
            if r < np.exp(-E_delta/T):
                E += E_delta
                pygame.draw.rect(window, colors[spin[rand_i, rand_j]], (rand_i * size, rand_j * size, size, size))
            else:
                spin[rand_i, rand_j] = spin[rand_i, rand_j] * -1

    # *** Clear the bottom margin and display:
    # temperature (T)
    # external field (H)
    # magnetization per spin (M/N)
    # energy per spin (E/N)

    M = np.sum(spin)/N
    avg_energy = E/N

    temp = font.render(f"Temperature: {T:.3f}", True, (255, 255, 255))
    field = font.render(f"External Field: {H:.3f}", True, (255, 255, 255))
    mag = font.render(f"Magnetization: {M:.3f}", True, (255, 255, 255))
    energy = font.render(f"Average Energy: {avg_energy:.3f}", True, (255, 255, 255))

    # *** Use key state check below to change temperature and external magnetic field
    keys = pygame.key.get_pressed()
    # I suggest q/a for coarse temp adjustment and w/s for fine temp adjustment.
    # Similarly, i/k and o/l for coarse and fine adjustment of external field.

    # Coarse Temp Adjust
    if keys[pygame.K_q]:
        T += 0.1
    if keys[pygame.K_a]:
        T -= 0.1
        if T < 0:
            T = 0

    # Fine Temp Adjust
    if keys[pygame.K_w]:
        T += 0.05
    if keys[pygame.K_s]:
        T -= 0.05
        '''
        if T < 0:
            T = 0
        '''
    # Coarse Ext Field Adjust
    if keys[pygame.K_i]:
        H += 0.1
    if keys[pygame.K_k]:
        H -= 0.1

    # Fine Ext Field Adjust
    if keys[pygame.K_o]:
        H += 0.05
    if keys[pygame.K_l]:
        H -= 0.05

    # Update the display
    window.blit(temp, (0, 800))
    window.blit(mag, (325, 800))
    window.blit(field, (0, 850))
    window.blit(energy, (325, 850))
    pygame.display.flip()
    t = clock.tick(fps)
    # Uncheck the print statement below to monitor ratio of tries to frame.
    # Close to 1 is ideal.  If too high, reduce ntries.  If too low, increase ntries.
    print(t*fps/1000)
```
<iframe width="1904" height="768" src="https://www.youtube.com/embed/LKIM1-Lr1ug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
