# Problem 2
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Define the differential equation for the forced damped pendulum
def forced_damped_pendulum(t, y, b, g, L, A, omega):
    """
    Differential equation governing the motion of a forced damped pendulum.
    
    Parameters:
    t : float
        Time variable.
    y : list
        State vector [theta, omega_dot].
    b : float
        Damping coefficient.
    g : float
        Gravitational acceleration.
    L : float
        Length of the pendulum.
    A : float
        Forcing amplitude.
    omega : float
        Forcing frequency.
    
    Returns:
    dydt : list
        Time derivatives [dtheta/dt, domega/dt].
    """
    theta, omega_dot = y  # y[0] = theta, y[1] = d(theta)/dt
    dtheta_dt = omega_dot
    domega_dt = -b * omega_dot - (g / L) * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Define system parameters
b = 0.2  # Damping coefficient
g = 9.81  # Gravitational acceleration (m/s^2)
L = 1.0  # Length of the pendulum (m)
A = 1.5  # Forcing amplitude
omega = 2.0  # Forcing frequency

# Initial conditions
t_span = (0, 50)  # Time range
y0 = [0.1, 0]  # Initial angle (rad) and angular velocity (rad/s)
t_eval = np.linspace(t_span[0], t_span[1], 1000)

# Solve the differential equation using numerical integration
sol = solve_ivp(forced_damped_pendulum, t_span, y0, t_eval=t_eval, args=(b, g, L, A, omega))

# Plot the time evolution of the pendulum's motion
plt.figure(figsize=(10, 5))
plt.plot(sol.t, sol.y[0], label='Theta (rad)')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.title('Forced Damped Pendulum Motion')
plt.legend()
plt.grid()
plt.show()

# Phase Space Diagram
plt.figure(figsize=(6, 6))
plt.plot(sol.y[0], sol.y[1], label='Phase Space')
plt.xlabel('Theta (rad)')
plt.ylabel('Angular Velocity (rad/s)')
plt.title('Phase Space Diagram')
plt.legend()
plt.grid()
plt.show()

# Poincaré Section
poincare_t = np.arange(0, t_span[1], 2 * np.pi / omega)  # Sample at driving period
poincare_theta = np.interp(poincare_t, sol.t, sol.y[0])
poincare_omega = np.interp(poincare_t, sol.t, sol.y[1])

plt.figure(figsize=(6, 6))
plt.scatter(poincare_theta, poincare_omega, color='red', s=10)
plt.xlabel('Theta (rad)')
plt.ylabel('Angular Velocity (rad/s)')
plt.title('Poincaré Section')
plt.grid()
plt.show()
