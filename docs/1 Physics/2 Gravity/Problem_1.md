# Orbital Period and Orbital Radius

## Motivation

The relationship between the square of the orbital period and the cube of the orbital radius, known as **Kepler's Third Law**, is a cornerstone of celestial mechanics. This simple yet profound relationship allows us to determine planetary motions and understand gravitational interactions on both local and cosmic scales. By analyzing this relationship, we can connect fundamental principles of gravity with real-world phenomena such as satellite orbits and planetary systems.

---

## Derivation of Kepler's Third Law for Circular Orbits

Consider a body of mass $m$ orbiting around a much more massive body of mass $M$ in a circular orbit of radius $r$.

From Newton's Law of Universal Gravitation:

$$
F_g = \frac{G M m}{r^2}
$$

From circular motion (centripetal force):

$$
F_c = \frac{m v^2}{r}
$$

Equating gravitational force to centripetal force:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Simplify:

$$
\frac{G M}{r} = v^2
$$

Orbital period $T$ is the time to complete one orbit:

$$
T = \frac{2\pi r}{v}
$$

Substitute $v$:

$$
T = \frac{2\pi r}{\sqrt{\frac{G M}{r}}} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Therefore:

$$
T^2 = \frac{4\pi^2}{G M} r^3
$$

This is **Kepler's Third Law**:

> The square of the orbital period is proportional to the cube of the orbital radius.

---
## Python Simulation of Circular Orbits


import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of Earth (kg)

# Orbital radii (in meters)
radii = np.linspace(1e7, 5e8, 100)  # from 10,000 km to 500,000 km

# Compute orbital periods using Kepler's Third Law
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

# Plotting
plt.figure(figsize=(8,6))
plt.plot(radii / 1e6, periods / 3600, label=r'$T \propto r^{3/2}$')  # hours
plt.xlabel('Orbital Radius (x $10^6$ m)')
plt.ylabel('Orbital Period (hours)')
plt.title('Orbital Period vs Radius (Kepler\'s Third Law)')
plt.grid(True)
plt.legend()
plt.show()


![alt text](<Ekran Resmi 2025-03-26 14.54.17-4.png>)


