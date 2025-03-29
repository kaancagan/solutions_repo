# Problem 2  
## Investigating the Dynamics of a Forced Damped Pendulum

---

## 1. Motivation

The **forced damped pendulum** serves as a powerful model to explore nonlinear dynamical systems. When damping and external periodic forcing are introduced, the system exhibits a wide array of behaviors — from regular periodic motion to chaotic dynamics.

These systems are relevant in multiple domains:

- Mechanical systems (e.g., suspension bridges, engines)
- Electrical circuits (analogous RLC systems)
- Climate and biological rhythms

Introducing external periodic forcing adds two key parameters:

- **Forcing amplitude** ($F_0$)  
- **Driving frequency** ($\omega_d$)

Tuning these parameters reveals various behaviors such as:

- Resonant amplification
- Synchronization
- Quasiperiodicity
- Chaos

This understanding has practical uses in **energy harvesting**, **vibration isolation**, and **resonance mitigation**.

---

## 2. Theoretical Foundation

### 2.1. Governing Differential Equation

We start with Newton’s Second Law for rotational motion:

Let:
- $m$ = mass of the pendulum bob  
- $L$ = length of the pendulum  
- $\theta$ = angular displacement  
- $b$ = damping coefficient  
- $F_0 \cos(\omega_d t)$ = external periodic force

The equation of motion becomes:

$$
m L^2 \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + mgL \sin(\theta) = F_0 \cos(\omega_d t)
$$

Divide through by $mL^2$:

$$
\frac{d^2\theta}{dt^2} + \frac{b}{mL^2} \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = \frac{F_0}{mL^2} \cos(\omega_d t)
$$

Define:
- Natural frequency:  
  $$ \omega_0^2 = \frac{g}{L} $$
- Damping ratio:  
  $$ \gamma = \frac{b}{mL^2} $$
- Forcing amplitude (normalized):  
  $$ A = \frac{F_0}{mL^2} $$

Final form:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega_d t)
$$

This is a **nonlinear**, second-order, non-homogeneous differential equation.

---

### 2.2. Approximate Solution for Small Angles

For small $\theta$, we use the **small-angle approximation**:

$$
\sin(\theta) \approx \theta
$$

Equation simplifies to:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega_d t)
$$

This is a **linear inhomogeneous** second-order ODE.

---

### 2.2.1. General Solution

The general solution has two parts:

#### a. Homogeneous Solution:

Solving the associated homogeneous equation:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = 0
$$

Its characteristic equation:

$$
r^2 + \gamma r + \omega_0^2 = 0
$$

Depending on $\gamma$, solutions are:

- **Underdamped** ($\gamma^2 < 4\omega_0^2$):

  $$
  \theta_h(t) = e^{-\gamma t / 2} \left( C_1 \cos(\omega_d' t) + C_2 \sin(\omega_d' t) \right)
  $$

  Where:

  $$
  \omega_d' = \sqrt{\omega_0^2 - \left( \frac{\gamma}{2} \right)^2}
  $$

- **Critically damped** and **overdamped** cases produce non-oscillatory decay.

---

#### b. Particular (Steady-State) Solution

We seek a solution of the form:

$$
\theta_p(t) = B \cos(\omega_d t - \delta)
$$

Where:
- $B$ = steady-state amplitude  
- $\delta$ = phase lag  

Amplitude is:

$$
B = \frac{A}{\sqrt{(\omega_0^2 - \omega_d^2)^2 + \gamma^2 \omega_d^2}}
$$

Phase lag:

$$
\tan(\delta) = \frac{\gamma \omega_d}{\omega_0^2 - \omega_d^2}
$$

---

### 2.3. Resonance and Energy Considerations

**Resonance** occurs when driving frequency approaches natural frequency:

$$
\omega_d \approx \omega_0
$$

At resonance, the amplitude becomes:

$$
B_{\text{max}} = \frac{A}{\gamma \omega_0} \quad \text{(approx. when } \omega_d = \omega_0 \text{)}
$$

Implications:

- Small damping $\Rightarrow$ large amplitudes (possible instability)
- Large damping $\Rightarrow$ suppressed resonance

**Total mechanical energy** of the pendulum:

$$
E(t) = \frac{1}{2} m L^2 \left( \frac{d\theta}{dt} \right)^2 + mgL (1 - \cos(\theta))
$$

Energy is maximized at resonance. Damping plays a critical role in dissipating energy and avoiding structural damage.

---

## Summary

The forced damped pendulum showcases a variety of dynamic behaviors based on system parameters. Its equation demonstrates how **nonlinear dynamics**, **resonance**, and **chaotic motion** can emerge even from a seemingly simple system.

---

![alt text](<Ekran Resmi 2025-03-29 14.31.19.png>)
![alt text](<Ekran Resmi 2025-03-29 14.31.33.png>)


## Code Explanation: Forced Damped Pendulum Simulation

---

### 1. Parameters

We begin by defining the **physical constants** and **initial conditions** for the pendulum system:

- **Gravitational acceleration**:  
  $$
  g = 9.81 \, \text{m/s}^2
  $$

- **Pendulum length**:  
  $$
  L = 1.0 \, \text{m}
  $$

- **Damping coefficient**:  
  $$
  \gamma = 0.1 \, \text{s}^{-1}
  $$

- **Forcing amplitude**:  
  $$
  A = 1.2
  $$

- **Driving frequency**:  
  $$
  \omega_d = \omega_0 = \sqrt{\frac{g}{L}} \approx 3.13 \, \text{rad/s}
  $$

This matches the **natural frequency** to investigate **resonance** conditions.

---

### 2. Initial Conditions

We start the simulation with:

- Initial angle (displacement):  
  $$
  \theta(0) = 0.1 \, \text{rad}
  $$

- Initial angular velocity:  
  $$
  \dot{\theta}(0) = 0.0 \, \text{rad/s}
  $$

---

### 3. ODE System Definition

We model the system using the second-order nonlinear ODE:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega_d t)
$$

This is rewritten as a first-order system:

Let:
- $x_1 = \theta$ (angle)
- $x_2 = \dot{\theta}$ (angular velocity)

Then:

$$
\begin{cases}
\frac{dx_1}{dt} = x_2 \\
\frac{dx_2}{dt} = -\gamma x_2 - \omega_0^2 \sin(x_1) + A \cos(\omega_d t)
\end{cases}
$$

This system is implemented in code via a function like:


def pendulum_derivatives(t, state):
    theta, omega = state
    dtheta_dt = omega
    domega_dt = -gamma * omega - (g / L) * np.sin(theta) + A * np.cos(omega_d * t)
    return np.array([dtheta_dt, domega_dt])

![alt text](<Ekran Resmi 2025-03-29 14.39.35-3.png>)

![alt text](<Ekran Resmi 2025-03-29 14.39.46.png>)

![alt text](<Ekran Resmi 2025-03-29 14.39.54.png>)

![alt text](<Ekran Resmi 2025-03-29 14.40.01.png>)

# Forced Damped Pendulum Simulation

This simulation investigates the dynamic behavior of a **forced damped pendulum** using Python's scientific libraries: `NumPy`, `Matplotlib`, and `SciPy`. The goal is to visualize the system's response under various damping and forcing conditions.

---

## 1. Setup

The simulation initializes with the following parameters:

- **Gravitational acceleration**:  
  $$
  g = 9.81 \, \text{m/s}^2
  $$

- **Pendulum length**:  
  $$
  L = 1.0 \, \text{m}
  $$

- **Damping coefficients**:  
  $$
  \gamma = \frac{b}{L}, \quad \text{where } b \in \{0.1, 0.5, 1.0\}
  $$

- **Forcing amplitudes**:  
  $$
  F_0 \in \{0.5, 1.2, 2.0\}
  $$

- **Driving frequencies**:  
  $$
  \omega_d \in \{1.0, 2.0, 3.0\}
  $$

- **Natural frequency**:  
  $$
  \omega_0 = \sqrt{\frac{g}{L}} \approx 3.13 \, \text{rad/s}
  $$

---

## 2. Governing Equations

The system is described by a nonlinear second-order differential equation:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = F_0 \cos(\omega_d t)
$$

Rewriting as a system of first-order equations:

- Let $\theta$ be the angle  
- Let $\omega = \frac{d\theta}{dt}$ be the angular velocity

Then:

$$
\frac{d\theta}{dt} = \omega
$$

$$
\frac{d\omega}{dt} = -\gamma \omega - \omega_0^2 \sin(\theta) + F_0 \cos(\omega_d t)
$$

---

## 3. Numerical Simulation

- Numerical integration is performed using the **Runge-Kutta 4(5)** method via `solve_ivp`.
- Simulation time span: $t \in [0, 50]$ seconds  
- Initial conditions:  
  $$
  \theta(0) = 0.1 \, \text{rad}, \quad \omega(0) = 0 \, \text{rad/s}
  $$

---

## 4. Visualization

### a. Angular Displacement

- Plots $\theta(t)$ for each combination of $b$, $F_0$, and $\omega_d$.
- Demonstrates how damping and external forcing affect the pendulum's motion.

### b. Phase Portrait

- Plots $\omega$ vs. $\theta$ for one representative case.
- Illustrates the system's trajectory in **phase space**.

### c. Poincaré Section

- A discrete sampling of the phase space:
  $$
  \left(\theta(t_n), \omega(t_n)\right) \quad \text{for every 20th time step}
  $$
- Useful for detecting periodicity or chaos.

### d. Bifurcation Diagram

- Varies driving frequency $\omega_d \in [0.5, 3.0]$.
- For each $\omega_d$, records final 50 values of $\theta(t)$.
- Reveals transitions between periodic and chaotic regimes.

---

## 5. Discussion

### Limitations

- **No small-angle approximation**: The full nonlinear $\sin(\theta)$ is used.
- **Damping is linear**: Realistic damping may be velocity-squared (quadratic).
- **External forcing** is idealized as perfectly periodic.

### Possible Extensions

- **Nonlinear damping**:  
  Include terms like $-k \omega^2 \operatorname{sign}(\omega)$ to better reflect air resistance.

- **Stochastic forcing**:  
  Add noise to the forcing function to simulate real-world irregularities:
  $$
  F_0 \cos(\omega_d t) + \text{random noise}
  $$

- **Coupled pendulums**:  
  Expand to multiple pendulums interacting to explore **multi-degree-of-freedom** systems.

