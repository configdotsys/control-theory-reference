# Solving State-Space Systems: Time-Domain vs Laplace-Domain

*Author: Percival Segui*

*Prepared as an independent technical reference.*

---

## Switching Between Time-Domain and Laplace-Domain

| Concept           | Time-Domain                       | Laplace-Domain                |
| ----------------- | --------------------------------- | ----------------------------- |
| State equation    | $\dot{x}(t) = A x(t) + B u(t)$    | $(sI - A)X(s) = x(0) + BU(s)$ |
| Output equation   | $y(t) = C x(t) + D u(t)$          | $Y(s) = C X(s) + D U(s)$      |
| Initial condition | Applied at $t = 0$                | Included as $x(0)$ in RHS     |
| Input $e^{-at}$   | $u(t) = e^{-at}$                  | $U(s) = \frac{1}{s + a}$      |
| Solve method      | Matrix exponentials & convolution | Algebraic manipulation        |

---

## Cramer’s Rule in Laplace-Domain (2x2 and 3x3 systems)

Given:

$$
(sI - A)X(s) = b(s), \quad \text{where } b(s) = x(0) + BU(s)
$$

To solve for $X_i(s)$:

1. Form matrix $M(s) = sI - A$
2. Replace column $i$ with $b(s)$ to get matrix $M_i(s)$
3. Compute:

$$
X_i(s) = \frac{\det M_i(s)}{\det M(s)} = \frac{\det M_i(s)}{\Delta(s)}
$$

Tips:

* $\Delta(s) = \det(sI - A)$ is always your common denominator
* Use symbolic algebra to expand numerators
* Perform partial fractions to invert to $x_i(t)$

---

### Worked Example (2x2 System)

Let:

$$
A = \begin{bmatrix} 0 & 1 \\ -4 & -5 \end{bmatrix}, \quad B = \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \quad x(0) = \begin{bmatrix} 2 \\ 1 \end{bmatrix}, \quad u(t) = 1 \Rightarrow U(s) = \frac{1}{s}
$$

Then:

$$
M(s) = sI - A = \begin{bmatrix} s & -1 \\ 4 & s+5 \end{bmatrix}, \quad b(s) = \begin{bmatrix} 2 \\ 1 + \frac{1}{s} \end{bmatrix}
$$

$$
\Delta(s) = \det(M) = s(s+5) + 4 = s^2 + 5s + 4
$$

Replace columns using Cramer's Rule:

**$X_1(s):$**

$$
\frac{\det\begin{bmatrix} 2 & -1 \\ 1 + \frac{1}{s} & s+5 \end{bmatrix}}{s^2 + 5s + 4} = \frac{2(s+5) - (-1) + \frac{1}{s}}{s^2 + 5s + 4} = \frac{2s + 11 + \frac{1}{s}}{s^2 + 5s + 4}
$$

Combine terms and perform partial fraction expansion as needed.

---

### Worked Example (3x3 System)

$$
A = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -24 & -26 & -9 \end{bmatrix}, \quad B = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}, \quad x(0) = \begin{bmatrix} 1 \\ 0 \\ 2 \end{bmatrix}, \quad u(t) = e^{-t} \Rightarrow U(s) = \frac{1}{s+1}
$$

$$
M(s) = sI - A = \begin{bmatrix} s & -1 & 0 \\ 0 & s & -1 \\ 24 & 26 & s+9 \end{bmatrix}, \quad b(s) = x(0) + \frac{1}{s+1} B = \begin{bmatrix} 1 \\ 0 \\ 2 + \frac{1}{s+1} \end{bmatrix}
$$

Compute $\Delta(s) = \det M(s) = s^3 + 9s^2 + 26s + 24$

Then apply Cramer’s Rule column-by-column:

$$
X_1(s) = \frac{\det M_1(s)}{\Delta(s)}, \quad X_2(s) = \frac{\det M_2(s)}{\Delta(s)}, \quad X_3(s) = \frac{\det M_3(s)}{\Delta(s)}
$$

---

## When to Use Laplace Over Time-Domain

| Scenario                             | Use Laplace? | Use Time-Domain?    |
| ------------------------------------ | ------------ | ------------------- |
| Step/exp input + initial condition   | Yes        | Avoid integrals   |
| System analysis (eigenvalues, poles) | Yes        | Not transparent   |
| Symbolic controller design           | Often      | Sometimes         |
| Simulation (MATLAB/Python)           | Yes        | Only to visualize |
| Academic modal insight               | Optional   | Yes               |

---

## Tips for Solving by Laplace + Cramer

* Always compute $\Delta(s) = \det(sI - A)$ first — this is your denominator

* Form $b(s) = x(0) + BU(s)$ carefully (don’t confuse initial condition and input!)

* If input is $u(t) = e^{-t}$, then $BU(s) = B \cdot \frac{1}{s + 1}$

* Each $X_i(s)$ comes from replacing one column of $M(s)$ with $b(s)$

* Expand numerator and simplify. If needed, use symbolic tools.

* For output: apply $Y(s) = C X(s) + D U(s)$

* Use inverse Laplace via partial fractions to get $x(t), y(t)$

---

## Final Advice

* Time-domain solutions build intuition
* Laplace-domain solutions solve problems
* Cramer’s Rule is your bridge between structure and answer

Once you know the Laplace framework, you rarely need to compute $e^{At}$ or integrals by hand.
