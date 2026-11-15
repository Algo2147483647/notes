# Mechanics of absolute spacetime

[TOC]

## Absolute spacetime

Absolute spacetime refers to the idea that space and time exist as independent, unchanging entities, separate from the matter and events that occur within them.

- **Space** is a fixed, uniform, infinite, three-dimensional backdrop where objects are located and distances are measured.
- **Time** is a continuous, one-dimensional flow that ticks the same for everyone, regardless of how they move.

### Coordinate transformation: Galileo's principle of relativity

Galileo's Principle of Relativity asserts the laws of physics are the same in all inertial reference frames. An **inertial reference frame** is one that is not accelerating, meaning it moves at a constant velocity (or is at rest). The transformation relationship between different inertial reference frames:

$$
\begin{align*}
t &= t' \tag{Time invariance}\\
\boldsymbol r &= \boldsymbol r' + \boldsymbol Vt  \tag{Position transformation}\\
\boldsymbol v &= \boldsymbol v' + \boldsymbol V  \tag{Velocity transformation}\\
\end{align*}
$$

- **Time invariance**: Time is absolute and does not change between inertial frames in Galilean relativity.
- **Position transformation**: the position in the original frame $\boldsymbol r$ is related to the position in the moving frame $\boldsymbol r'$ by adding the distance the moving frame has traveled during time $t$, which is $\boldsymbol V t$.
- **Velocity transformation**: the velocity of an object in the original frame $\boldsymbol v$ is the sum of its velocity in the moving frame $\boldsymbol v'$ and the velocity of the moving frame itself $\boldsymbol V$.

#### Coordinate transformation between non-inertial coordinate systems: Fictitious Force

Non-inertial reference frames accelerate relative to an inertial reference frame. In these systems, Newton's laws of motion do **not** hold without including fictitious forces. Transformations must account for relative acceleration and rotational effects. Let:
- $S$: Inertial frame (stationary or moving with constant velocity).
- $S'$: Non-inertial frame, accelerating or rotating relative to $S$.

The general transformation depends on **relative motion**:

- Translational acceleration ($\vec{a}_\text{rel}$).
- Rotational motion (angular velocity $\vec{\omega}$ and angular acceleration $\vec{\alpha}$).
$$
\begin{align*}
\vec{r} &= \vec{r}' + \vec{R}(t)\\
\vec{v} &= \vec{v}' + \vec{V}(t) + \vec{\omega} \times \vec{r}' \\
\vec{a} &= \vec{a}' + \vec{A}(t) + 2 \vec{\omega} \times \vec{v}' + \vec{\omega} \times (\vec{\omega} \times \vec{r}') + \vec{\alpha} \times \vec{r}'
\end{align*}
$$

- $\vec{R}(t)$ is the time-dependent displacement of $S'$ relative to $S$.
- $\vec{v}'$: Velocity in the non-inertial frame.
- $\vec{V}(t)$: Velocity of $S'$ relative to $S$.
- $\vec{\omega} \times \vec{r}'$: Contribution due to rotation 
- $\vec{a}$: Acceleration in the inertial frame.
- $\vec{a}'$: Acceleration in the non-inertial frame.
- $\vec{A}(t)$: Acceleration of $S'$ relative to $S$.
- $2\vec{\omega} \times \vec{v}'$: **Coriolis force** term.
- $\vec{\omega} \times (\vec{\omega} \times \vec{r}')$: **Centrifugal force** term.
- $\vec{\alpha} \times \vec{r}'$: Contribution due to angular acceleration.

| **Fictitious Force**    | **Expression**                     | **Cause**                  |
|--------------------------|------------------------------------|----------------------------|
| Centrifugal Force        | $\vec{F}_\text{cent} = -m (\vec{\omega} \times (\vec{\omega} \times \vec{r}))$ | Rotation of $S'$       |
| Coriolis Force           | $\vec{F}_\text{cor} = -2m (\vec{\omega} \times \vec{v}')$ | Relative velocity in $S'$ |
| Linear Acceleration Force| $\vec{F}_\text{lin} = -m \vec{A}(t)$  | Translational acceleration |
| Angular Acceleration Force| $\vec{F}_\text{ang} = -m (\vec{\alpha} \times \vec{r}')$ | Angular acceleration       |

## Action

### Action of particles

$$
\begin{align*}
S &= \int (T - V) \mathrm dt  \\
S &= \int \left(\frac{m v^2}{2} - U(\boldsymbol r, t)\right) \mathrm dt  \tag{particle}\\
S &= \int \sum\frac{m_i v_i^2}{2} \mathrm dt  \tag{Free particle system}
\end{align*}
$$

### Equations of motion

$$
\boldsymbol F = \frac{\mathrm{d} \boldsymbol P}{\mathrm{d}t} = m \frac{\mathrm{d} \boldsymbol v}{\mathrm{d}t}\\
\boldsymbol F = - \frac{\partial U(\boldsymbol r, t)}{\partial \boldsymbol r}
$$

An isolated particle remains stationary or moves in a uniform straight line without the action of an external force. For a particle with momentum $\boldsymbol P$, the rate of change of its momentum with time is proportional to the external force on the particle and has the same direction as the external force. 

The action and reaction forces between two interacting particles are always equal in magnitude, opposite in direction, and act on the same straight line.
$$
\boldsymbol F_{12} = - \boldsymbol F_{21}
$$

### Conserved quantity: Momentum, Angular momentum, Energy

$$
\begin{align*}
\boldsymbol P &= m \frac{\mathrm{d} \boldsymbol r}{\mathrm{d}t}  \tag{Momentum }\\
\boldsymbol L &= \boldsymbol r \times \boldsymbol P  \tag{Angular Momentum}\\
E &= \frac{1}{2} mv^2  \tag{Kinetic Energy}\\
\end{align*}
$$

- **Momentum** is a vector quantity that describes the motion of an object.
- **Angular momentum** is a vector quantity that describes the rotational motion of an object about a point or an axis.
- **Kinetic Energy**: The energy associated with an object's motion.

### Rigid body

- 

## Gravitation

$$
\boldsymbol F = \frac{G m_1m_2}{r^2}\hat{\boldsymbol r} \\
U = \frac{G m_1m_2}{r}
$$

- $G$: Gravitational constant. $G = (6.67 \pm0.07) \times 10^{-11} \mathrm{m^3kg^{-1}s^{-2}}$

### Two-body gravitational system

When one particle is stationary as the origin, the trajectory equation of the other particle is as follows. Among them, the polar coordinate equation of the conic section, the $e$ eccentricity, and the $p$ semi-diameter. The two-body scenario can be abstracted as motion around the equivalent center of mass in an inertial system.
$$
\begin{align*}
  r &= \frac{p}{1 - e \sin(θ + θ_0)}  \\
  p &= \frac{L^2}{G M m^2}  \\
  e &= \sqrt{1 + 2 \frac{E}{m} \left(\frac{L}{G M m}\right)^2}
\end{align*}
$$

### Restricted three-body gravitational system
两个大质量天体 $M_1, M_2$, 选择以质心为原点且使其相对静止的旋转参考系, 则势能有, 
$$
\begin{align*}
U &= -\frac{GM_1}{r_1} -\frac{GM_1}{r_2} - \frac{1}{2} \omega^2 r^2\\
\omega &= \sqrt{\frac{G(M_1+M_2)}{d^3}}\\
r_1 &= \sqrt{(x + \frac{M_2}{M_1+M_2}d)^2 + y^2}\\
r_2 &= \sqrt{(x - \frac{M_1}{M_1+M_2}d)^2 + y^2}
\end{align*}
$$

#### Lagrange Points

Lagrange points are points of equilibrium for small-mass objects under the gravitational influence of two massive orbiting bodies. Mathematically, this involves the solution of the restricted three-body problem. 拉格朗日点的条件
$$
\nabla U = 0
$$

$$
\begin{align*}
L_1 &= \left(-\frac{M_2}{M_1 + M_2}d , 0\right)\\
L_2 &= \left(+\frac{M_1}{M_1 + M_2}d , 0\right)\\
L_3 &= \left(-\frac{M_1}{M_1 + M_2}d , 0\right)\\
L_4 &= \left(\frac{M_1 - M_2}{M_1 + M_2}d, +\frac{\sqrt{3}}{2} d\right)\\
L_5 &= \left(\frac{M_1 - M_2}{M_1 + M_2}d, -\frac{\sqrt{3}}{2} d\right)\\
\end{align*}
$$

