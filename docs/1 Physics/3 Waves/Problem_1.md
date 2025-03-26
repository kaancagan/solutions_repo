# Interference Patterns on a Water Surface

## Motivation

When waves from multiple sources meet on a water surface, they **interfere** — adding or canceling each other depending on their phase. This project simulates interference patterns from **coherent point sources** placed at the vertices of a **regular polygon**.

---

## Problem Setup

We simulate wave interference from 4 coherent sources placed at the vertices of a **square**. Each source emits circular waves of the same frequency, amplitude, and phase. The resulting displacement at each point on the water surface is given by:

$$
u(x, y, t) = \sum_{i=1}^{N} A \cdot \sin(k r_i - \omega t + \phi)
$$

Where:
- $A$: amplitude
- $k = \frac{2\pi}{\lambda}$: wave number
- $\omega = 2\pi f$: angular frequency
- $r_i$: distance from source $i$ to point $(x, y)$
- $N$: number of sources

---

## Python Simulation
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0               # Amplitude
λ = 1.0               # Wavelength (meters)
f = 1.0               # Frequency (Hz)
ω = 2 * np.pi * f     # Angular frequency
k = 2 * np.pi / λ     # Wave number
φ = 0                 # Initial phase
N = 4                 # Number of sources (square)

# Grid setup
grid_size = 200
x = np.linspace(-5, 5, grid_size)
y = np.linspace(-5, 5, grid_size)
X, Y = np.meshgrid(x, y)

# Polygon vertices (square centered at origin, side length 4)
side = 4
L = side / np.sqrt(2)
sources = [
    (-L, -L),
    (-L, L),
    (L, -L),
    (L, L)
]

# Time snapshot
t = 0  # You can change this or animate over time

# Superpose waves from all sources
U = np.zeros_like(X)
for (x0, y0) in sources:
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    U += A * np.sin(k * r - ω * t + φ)

# Plotting
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, U, levels=100, cmap='viridis')
plt.colorbar(label='Wave Displacement')
plt.scatter(*zip(*sources), color='red', label='Sources')
plt.title('Wave Interference Pattern (Square Configuration)')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.legend()
plt.axis('equal')
plt.grid(False)
plt.show()


![alt text](<Ekran Resmi 2025-03-26 15.32.18.png>)

## Observations

- The **bright** regions correspond to **constructive interference** (waves reinforcing).
- The **dark** regions are areas of **destructive interference** (waves cancelling).
- The symmetric pattern arises from the **square geometry** of the source placement.

---

## Next Steps

- Try other polygons: triangle (3), pentagon (5), hexagon (6)
- Animate the surface: simulate time evolution with `t` varying
- Try random phases or incoherent sources

---

## Conclusion

This simulation shows how simple wave equations can create beautiful and complex **interference patterns**. Understanding these patterns helps explain physical phenomena from sound and light to quantum waves.

> 💧 "Where waves meet, patterns emerge."  
