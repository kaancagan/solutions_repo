# Escape Velocities and Cosmic Velocities

## Motivation

The concept of **escape velocity** is fundamental in understanding how to overcome a celestial body's gravitational pull. Expanding on this, the **first**, **second**, and **third cosmic velocities** describe the minimum speeds needed to:
1. Maintain a circular orbit (1st cosmic velocity),
2. Escape the body's gravity (2nd cosmic velocity),
3. Escape the solar system (3rd cosmic velocity).

These principles guide space missions from satellite launches to interplanetary and interstellar exploration.

---

## Definitions of Cosmic Velocities

### First Cosmic Velocity ($v_1$)
- The minimum velocity required for an object to enter a stable circular orbit around a celestial body.
- Derived from: $\frac{G M}{r} = v_1^2$

$$
v_1 = \sqrt{\frac{G M}{r}}
$$

### Second Cosmic Velocity ($v_2$)
- The **escape velocity**, or the speed needed to completely break free from a celestial body's gravity.

$$
v_2 = \sqrt{2} \cdot v_1 = \sqrt{\frac{2 G M}{r}}
$$

### Third Cosmic Velocity ($v_3$)
- The speed needed to escape not just the planet, but also its parent star's gravity (e.g., Earth + Sun).

Approximate (simplified):

$$
v_3 \approx \sqrt{v_{sun}^2 + v_2^2}
$$

Where $v_{sun}$ is the orbital speed of the planet around the Sun.

---

## Python Implementation and Visualization


import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)

# Celestial bodies: (mass in kg, radius in m)
bodies = {
    "Earth": {"M": 5.972e24, "R": 6.371e6, "v_sun": 29.78e3},
    "Mars": {"M": 6.417e23, "R": 3.3895e6, "v_sun": 24.07e3},
    "Jupiter": {"M": 1.898e27, "R": 6.9911e7, "v_sun": 13.07e3}
}

# Compute velocities
results = {}
for name, data in bodies.items():
    M = data["M"]
    R = data["R"]
    v1 = np.sqrt(G * M / R)
    v2 = np.sqrt(2) * v1
    v3 = np.sqrt(v2**2 + data["v_sun"]**2)
    results[name] = {"v1": v1, "v2": v2, "v3": v3}

# Display results
for name, v in results.items():
    print(f"\n{name}:")
    print(f"  First Cosmic Velocity (Orbit): {v['v1'] / 1000:.2f} km/s")
    print(f"  Second Cosmic Velocity (Escape): {v['v2'] / 1000:.2f} km/s")
    print(f"  Third Cosmic Velocity (Interstellar): {v['v3'] / 1000:.2f} km/s")

# Plotting
labels = list(results.keys())
v1_vals = [results[body]['v1'] / 1000 for body in labels]
v2_vals = [results[body]['v2'] / 1000 for body in labels]
v3_vals = [results[body]['v3'] / 1000 for body in labels]

x = np.arange(len(labels))
width = 0.25

plt.figure(figsize=(10,6))
plt.bar(x - width, v1_vals, width, label='v1 (Orbit)')
plt.bar(x, v2_vals, width, label='v2 (Escape)')
plt.bar(x + width, v3_vals, width, label='v3 (Solar Escape)')

plt.ylabel('Velocity (km/s)')
plt.title('Cosmic Velocities for Earth, Mars, and Jupiter')
plt.xticks(x, labels)
plt.legend()
plt.grid(True, axis='y')
plt.tight_layout()
plt.show()

![alt text](<Ekran Resmi 2025-03-26 15.11.08-1.png>)


![alt text](<Ekran Resmi 2025-03-26 15.11.24.png>)