# Problem 1  
## Orbital Period and Orbital Radius

---

## 1. Motivation

**Kepler’s Third Law** states that the square of the orbital period $T$ of a planet is proportional to the cube of its orbital radius $r$ (semi-major axis in elliptical orbits). This relationship is derived from **Newton’s Law of Universal Gravitation** and **centripetal force balance** in circular motion.

This document will:

- Derive the relationship between $T$ and $r$
- Discuss astronomical implications
- Implement a computational model
- Visualize the $T$–$r$ relationship

---

## 2. Derivation of Kepler’s Third Law (Circular Orbits)

### Newton’s Law of Universal Gravitation:

$$
F_g = \frac{G M m}{r^2}
$$

Where:
- $G$ is the gravitational constant
- $M$ is the mass of the central body (e.g., Sun)
- $m$ is the mass of the orbiting object (e.g., planet)
- $r$ is the orbital radius

### Centripetal Force (for circular motion):

$$
F_c = \frac{m v^2}{r}
$$

Setting $F_g = F_c$:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Cancel $m$:

$$
\frac{G M}{r^2} = \frac{v^2}{r}
$$

Rearranged:

$$
v^2 = \frac{G M}{r}
$$

Orbital period is:

$$
T = \frac{2\pi r}{v}
$$

Substitute $v$:

$$
T = \frac{2\pi r}{\sqrt{\frac{G M}{r}}} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

**Squaring both sides:**

$$
T^2 = \frac{4\pi^2 r^3}{G M}
$$

---

## 3. Implications of Kepler’s Third Law

### 3.1 Determining Mass of Celestial Bodies

Rearranged:

$$
M = \frac{4\pi^2 r^3}{G T^2}
$$

#### Example: Mass of the Sun

Using Earth’s values:
- $r = 1 \, \text{AU} = 1.496 \times 10^{11} \, \text{m}$
- $T = 365.25 \, \text{days} = 3.156 \times 10^7 \, \text{s}$

Plug into the formula to estimate the Sun’s mass.

---

### 3.2 Estimating Distances to Moons and Planets

Given:

$$
T^2 \propto r^3
$$

We can compute $r$ from measured $T$:

$$
r = \left( \frac{G M T^2}{4\pi^2} \right)^{1/3}
$$

#### Example: Jupiter’s Moons

Galileo observed their periods. Applying this relation gave their distances — a foundational method still used for **exoplanets** today.

---

### 3.3 Satellite Motion and Geostationary Orbits

Satellites orbit Earth according to Kepler’s law. For **geostationary orbit**, $T = 24$ hours:

$$
r = \left( \frac{G M_\text{Earth} T^2}{4\pi^2} \right)^{1/3}
$$

This gives:

$$
r \approx 4.22 \times 10^7 \, \text{m}
$$

Subtracting Earth’s radius:

$$
\text{Altitude} \approx 35,786 \, \text{km}
$$

---

### 3.4 Exoplanet Discovery

**Transit Method**: Measures $T$ as a planet passes in front of a star  
**Radial Velocity Method**: Detects periodic shifts in starlight

Apply:

$$
r^3 = \frac{G M T^2}{4\pi^2}
$$

Used in NASA’s **Kepler Telescope** to detect thousands of planets.

---

### 3.5 Binary Star Systems & Black Holes

Kepler’s Law works for two orbiting stars:

$$
T^2 = \frac{4\pi^2 r^3}{G (M_1 + M_2)}
$$

#### Example: Cygnus X-1

The orbit of a visible star around an invisible companion led to the discovery of a black hole via its inferred mass.

---

### 3.6 Galactic Structure and Dark Matter

Kepler’s Law predicts orbital velocity:

$$
v = \sqrt{\frac{G M}{r}} \Rightarrow v \propto \frac{1}{\sqrt{r}}
$$

But observations show **flat rotation curves**:

$$
v \approx \text{constant}
$$

This implies:

$$
M(r) \propto r
$$

**Evidence for dark matter** — unseen mass influencing galactic dynamics.

---

## 4. Summary

- Kepler’s Third Law relates $T^2 \propto r^3$
- Enables measurement of masses, distances, and orbits
- Essential in astronomy, satellite technology, and exoplanet research
- Deviations in galaxies suggest presence of **dark matter**

Real-World Example: Moon’s Orbit Around Earth

The Moon’s orbit around Earth follows Kepler’s Third Law. Given: - Earth’s mass , - Orbital radius of the Moon ,

we can compute its orbital period .

Computational Model

The following Python script simulates a circular orbit and verifies Kepler’s Third Law using numerical data.


![alt text](<Ekran Resmi 2025-03-29 14.51.19.png>)

![alt text](<Ekran Resmi 2025-03-29 14.51.51.png>)

# Explanation of the Code and Results

This section explains the Python code used to simulate **circular orbits** and verify **Kepler’s Third Law** through computational methods and visualizations.

---

## 1. Code Explanation

### a. Constants

The following constants are defined using standard astronomical values:

- Gravitational constant:  
  $$
  G = 6.67430 \times 10^{-11} \, \text{m}^3 \cdot \text{kg}^{-1} \cdot \text{s}^{-2}
  $$

- Mass of the Sun:  
  $$
  M_{\odot} = 1.989 \times 10^{30} \, \text{kg}
  $$

- Mass of the Earth:  
  $$
  M_{\oplus} = 5.972 \times 10^{24} \, \text{kg}
  $$

---

### b. Orbital Period Function

The orbital period is calculated using:

$$
T = \sqrt{\frac{4\pi^2 r^3}{G M}}
$$

- $r$: Orbital radius (m)  
- $M$: Mass of the central body (Sun or Earth)  
- $T$: Orbital period (converted from seconds to days for readability)

---

### c. Verification Plot: \( T^2 \) vs. \( r^3 \)

- Computes $T^2$ and $r^3$ for orbits around both the Sun and Earth.
- Plots these values to verify the relation:

$$
T^2 \propto r^3
$$

- Since:

$$
T^2 = \frac{4\pi^2}{G M} \cdot r^3
$$

the graph should yield a straight line, where the slope is inversely proportional to the central mass ($M$).

---

### d. Orbit Simulation

The function `simulate_orbit(r, T)` uses parametric equations to simulate circular motion:

$$
x(t) = r \cos\left(\frac{2\pi t}{T}\right), \quad
y(t) = r \sin\left(\frac{2\pi t}{T}\right)
$$

- $t$: Time sampled over one complete period
- Describes **uniform circular motion**

Orbits simulated:

- Earth around the Sun  
- Moon around Earth

---

## 2. Results and Verification

### Plot 1: \( T \) vs. \( r \) (Log-Log Scale)

**Description:**
- A log-log plot confirms that:

$$
T \propto r^{3/2}
$$

- The straight lines indicate power-law behavior.

**Verification:**
- Linearity confirms Kepler’s Third Law.
- Slopes differ due to central mass:
  - Sun has a **shallower slope** (higher mass)
  - Earth has a **steeper slope** (lower mass)

---

### Plot 2: Circular Orbit Visualization

**Description:**
- Visual representation of two orbital paths:
  - Earth’s orbit around the Sun (wide circle)
  - Moon’s orbit around the Earth (smaller circle)

**Verification:**
- Orbits are visually circular, aligning with the assumption.
- Time periods match real values:
  - Earth:  
    $T_{\text{Earth}} \approx 365.25 \, \text{days}$
  - Moon:  
    $T_{\text{Moon}} \approx 27.32 \, \text{days}$

---

### Printed Output

Displayed numerical values:

- Orbital radii (m)
- Orbital periods (converted to days)

These match known astronomical data, providing confidence in the simulation.

---

## 3. Conclusion

✅ The code correctly models **circular orbital mechanics**  
✅ Log-log plot of $T$ vs. $r$ confirms **Kepler’s Third Law**  
✅ Circular orbit visualization helps **intuitively understand orbital motion**  
✅ Computed periods match **observational data**, reinforcing the model’s accuracy

---
