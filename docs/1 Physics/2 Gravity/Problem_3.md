# Trajectories of a Freely Released Payload Near Earth

## Motivation

When a payload is released from a moving rocket near Earth, its trajectory is governed by gravity and its initial velocity. The result could be:

- A **circular** or **elliptical** orbit (if speed is below escape velocity),
- A **parabolic** trajectory (if speed equals escape velocity),
- A **hyperbolic** trajectory (if speed exceeds escape velocity),
- Or a **reentry** if the speed is insufficient to sustain orbit.

These outcomes are critical for satellite deployment, deorbiting modules, and interplanetary missions.

---

## Theoretical Background

The motion of a payload near Earth is governed by **Newton's Law of Gravitation**:

$$
F = \frac{G M m}{r^2}
$$

This force causes **acceleration** toward Earth:

$$
\vec{a} = -\frac{G M}{r^2} \hat{r}
$$

Where:
- $G$ is the gravitational constant,
- $M$ is Earth's mass,
- $r$ is the distance to Earth's center.

The trajectory depends on the initial velocity vector $\vec{v}_0$. Depending on $|\vec{v}_0|$, the object may fall back, orbit, or escape.

---

## Python Simulation of Payload Trajectories

We use numerical integration (Euler or Runge-Kutta) to simulate the path.


import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M = 5.972e24     # kg (Earth)
R_earth = 6.371e6  # m (Earth radius)

# Time setup
dt = 1           # seconds
t_max = 10000    # total simulation time in seconds
steps = int(t_max / dt)

# Initial conditions
altitude = 400e3  # 400 km above Earth
r0 = np.array([R_earth + altitude, 0])  # initial position
speeds = [5000, 7670, 11000, 11200]     # vary speed to test different paths (m/s)
labels = ['Reentry', 'Stable Orbit', 'Escape', 'Hyperbolic']

def simulate_trajectory(v0_mag):
    r = r0.copy()
    v = np.array([0, v0_mag])
    traj = [r.copy()]

    for _ in range(steps):
        r_mag = np.linalg.norm(r)
        a = -G * M / r_mag**3 * r
        v += a * dt
        r += v * dt
        if r_mag < R_earth:
            break  # crashed
        traj.append(r.copy())
    return np.array(traj)

# Plot all trajectories
plt.figure(figsize=(8,8))
theta = np.linspace(0, 2*np.pi, 100)
earth_x = R_earth * np.cos(theta)
earth_y = R_earth * np.sin(theta)
plt.plot(earth_x, earth_y, 'b', label='Earth')

for v0, label in zip(speeds, labels):
    traj = simulate_trajectory(v0)
    plt.plot(traj[:,0], traj[:,1], label=f'{label} ({v0/1000:.1f} km/s)')

plt.axis('equal')
plt.grid(True)
plt.xlabel('X Position (m)')
plt.ylabel('Y Position (m)')
plt.title('Payload Trajectories from 400 km Altitude')
plt.legend()
plt.show()


![alt text](<Ekran Resmi 2025-03-26 15.26.17.png>)