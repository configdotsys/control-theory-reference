# Tangent-Line Linearization Procedure

*Use this when you want to approximate a nonlinear differential equation with a linear one near a known operating point.*

*This is tangent-line linearization, not necesarily equilibrium linearization.*

---

## General Form

You are given an equation of the form:

$$
\text{(linear terms)} + f(x) = 0
$$

Where:
- $f(x)$ is **nonlinear** (i.e., $\cos x$, $ ln x$, $e^x$, etc.)
- You want to linearize near a point $x_0$

---

## Step-by-Step Procedure

---

### Step 1: Identify the Operating Point

Pick the known value around which you want to analyze the system:

$$
x_0 = \text{operating point}
$$

---

### Step 2: Define the Deviation Variable

Let:

$$
\delta x(t) = x(t) - x_0
$$

This represents small changes around $ x_0 $.

---

### Step 3: Replace the Nonlinear Term with the Tangent Line Approximation

Use the **equation of the tangent line**:

$$
f(x) \approx f(x_0) + f'(x_0) \cdot (x - x_0) = f(x_0) + f'(x_0) \cdot \delta x
$$

This gives a **linear approximation** for $f(x)$ near $x_0$.

---

### Step 4: Plug into the Differential Equation

Substitute the approximation into the original equation:

$$
\text{(linear terms)} + f(x_0) + f'(x_0) \delta x = 0
$$

---

### Step 5: Subtract Off the Constant $ f(x_0) $

Move the constant term to the other side:

$$
\text{(linear terms)} + f'(x_0) \delta x = -f(x_0)
$$

Now your equation is fully linear in $\delta x$, and includes any necessary offset (forcing term) due to the original nonlinear shape.

---

## Clarifying Note on Operating Points and Forcing Terms

The appearance of the constant term $f(x_0)$ depends on how the operating point is chosen.

If $x_0$ is selected as an **equilibrium point** of the original nonlinear system, then it satisfies the steady-state condition:

$$
\text{(linear terms)} + f(x_0) = 0
$$

In this case, $f(x_0)=0$ when the system is expressed in deviation variables, and the linearized model describes **small-signal dynamics about equilibrium**. The resulting deviation equation is homogeneous.

If $x_0$ is **not** an equilibrium point, then $f(x_0)\neq 0$, and the linearized deviation equation includes a **constant forcing term**. This represents the fact that the original system would naturally accelerate away from that point even with zero deviation.

Both forms are mathematically valid:

* equilibrium linearization $\rightarrow$ small-signal dynamics
* non-equilibrium linearization $\rightarrow$ linear approximation with constant offset

The example shown below uses a non-equilibrium operating point to illustrate the general tangent-line procedure.

---

## Example

Original nonlinear equation:

$$
\frac{d^2 x}{dt^2} + 2 \frac{dx}{dt} + \cos x = 0
$$

Operating point: $x_0 = \frac{\pi}{4}$

Then:
- $f(x_0) = \cos(\frac{\pi}{4}) = \frac{\sqrt{2}}{2}$
- $f'(x_0) = -\sin(\frac{\pi}{4}) = -\frac{\sqrt{2}}{2}$

So:

$$
\cos x \approx \frac{\sqrt{2}}{2} - \frac{\sqrt{2}}{2} \cdot \delta x
$$

Substitute and subtract constant:

$$
\frac{d^2 \delta x}{dt^2} + 2 \frac{d \delta x}{dt} - \frac{\sqrt{2}}{2}\delta x = -\frac{\sqrt{2}}{2}
$$

This is the fully linearized version of the original equation.

---

## Summary Table

| Step | Description |
|------|-------------|
| 1 | Choose operating point $x_0$ |
| 2 | Define deviation: $\delta x = x - x_0$ |
| 3 | Approximate: $f(x) \approx f(x_0) + f'(x_0) \delta x$ |
| 4 | Plug into equation |
| 5 | Subtract constant $f(x_0)$ to isolate linear deviation |

> This gives a complete linear model, valid for small deviations around the point of interest.

---