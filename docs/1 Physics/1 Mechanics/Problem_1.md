# Investigating the Range as a Function of the Angle of Projection

## 1. Motivation

Projectile motion, though seemingly basic, offers a deep and insightful perspective into core physics concepts. The primary objective here is to explore how the **range** of a projectile varies as a function of the **angle of projection**. 

While the problem setup appears straightforward, it conceals a rich mathematical structure involving both linear and quadratic relationships. This topic is fascinating due to several influencing variables, such as:

- Initial velocity ($v_0$)
- Gravitational acceleration ($g$)
- Launch height ($h$)

Each of these parameters contributes to a wide array of physical trajectories — from a soccer ball's curved path to a space rocket's arc.

---

## 2. Theoretical Foundation

The equations governing projectile motion are derived using Newton’s Second Law:

### 2.1. Equations of Motion

In an idealized scenario (neglecting air resistance), the forces acting on a projectile are:

1. Gravitational force in the vertical direction  
2. No horizontal forces

From Newton’s laws:

- Horizontal acceleration: $$ a_x = 0 $$
- Vertical acceleration: $$ a_y = -g $$

Integrating over time $t$, we get the velocity components:

$$
v_x = v_0 \cos(\theta)
$$

$$
v_y = v_0 \sin(\theta) - gt
$$

Integrating again gives the position equations:

$$
x(t) = v_0 \cos(\theta) \cdot t
$$

$$
y(t) = v_0 \sin(\theta) \cdot t - \frac{1}{2}gt^2
$$

These define the horizontal (constant velocity) and vertical (accelerated) motions.

---

### 2.2. Time of Flight

To find the total time the projectile remains in the air, set $y(t) = 0$ (assuming launch and landing occur at the same height):

$$
t = \frac{2 v_0 \sin(\theta)}{g}
$$

---

### 2.3. Range Equation

The **range** $R$ is the total horizontal distance traveled before the projectile lands:

Using horizontal motion:

$$
R = v_0 \cos(\theta) \cdot t
$$

Substitute time of flight:

$$
R = v_0 \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g}
$$

Apply the identity:

$$
\sin(2\theta) = 2 \sin(\theta) \cos(\theta)
$$

Final equation for range:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

---

### 2.4. Maximum Range

The range is maximized when $\sin(2\theta)$ is at its peak value (which is 1):

$$
\theta = 45^\circ
$$

Therefore, the **maximum range** occurs at a launch angle of $45^\circ$ when launch and landing heights are the same.

---

## 3. Range Analysis

### 3.1. Dependence on Angle

- The function $R(\theta)$ is symmetric around $45^\circ$
- Angles $\theta$ and $90^\circ - \theta$ yield the same range

### 3.2. Effect of Initial Velocity

- The range increases **quadratically** with initial speed:

$$
R \propto v_0^2
$$

### 3.3. Effect of Gravitational Acceleration

- Higher gravity (e.g., Jupiter) → **shorter range**  
- Lower gravity (e.g., Moon) → **longer range**

---

## Summary

Projectile range is influenced by several physical parameters, but follows a clear mathematical structure. By understanding the role of each parameter, especially the angle of projection, one can predict and optimize the trajectory of various real-world projectiles.

---

Visualization with Air Resistance
![alt text](<Ekran Resmi 2025-03-29 14.20.44.png>)
