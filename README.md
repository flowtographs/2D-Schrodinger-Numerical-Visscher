# Numerical Simulation of the 2D Time-Dependent Schrödinger Equation
## [Visscher's Method](https://www.asc.tuwien.ac.at/~juengel/simulations/schroedinger/Visscher_method.html)

- We consider the following dimensionless representation of the time-dependent Schrödinger equation (TDSE), where the relevant physical scales are expressed in [Hartree units](https://en.wikipedia.org/wiki/Hartree_atomic_units) ($\hbar = m_{e} = a_{0} = 1$).
- 

$$
    i\frac{\partial \Psi}{\partial t} = \left(\frac{1}{2}{\nabla}^{2} + \mathbb{V}\right)\Psi 
$$

- At any of the points indexed within the discrete space and time domains, the solution to the TDSE is denoted 

$$
    \Psi(x_i, y_j, t_n) = \Psi_{i,j}^{n}
$$

- The numerical method we consider here is that developed by Visscher in 1991, wherein the wavefunction is separated into real and imaginary components and discretized over staggered times differing by a half-step. For $\Psi = u + iv$:

$$
    \Psi = u + i v \quad \implies \quad
    \begin{cases} 
        \dfrac{\partial u}{\partial t} = \mathbb{H}v\\
        \dfrac{\partial v}{\partial t} = -\mathbb{H}u
    \end{cases}
$$

- In terms of Finite-differences:

$$ u\left(x_{i}, y_{j}, t_{n}\right) \longrightarrow\quad u^{n}_{i,j} $$

$$ v\left(x_{i}, y_{j}, t_{n}-{\Delta t}/{2}\right) \longrightarrow\quad v^{n}_{i,j} $$

- Solving for the $n+1$ time-step:

$$ 
  v_{i,j}^{n+1} = v_{i,j}^{n} + \frac{\Delta t}{2\Delta x^{2}} \left( u_{i,j+1}^{n} + u_{i,j-1}^{n} + u_{i+1,j}^{n} + u_{i-1,j}^{n} - 4 u_{i,j}^{n} \right) - \Delta t V_{i,j} u_{i,j}^{n}
$$
  
$$
  u_{i,j}^{n+1} = u_{i,j}^{n} - \frac{\Delta t}{2\Delta x^{2}} \left( v_{i,j+1}^{n} + v_{i,j-1}^{n} + v_{i+1,j}^{n} + v_{i-1,j}^{n} - 4 v_{i,j}^{n} \right) + \Delta t V_{i,j} v_{i,j}^{n+1}
$$

- To ensure that the method is unitary, the probability density $|\Psi|^2$ is defined as:

$$
    P^{n} = u^{n} u^{n} + v^{n}v^{n+1}
$$

- The stability condition is
 
$$
    -\frac{2}{\Delta t} \leq V_{0} \leq \frac{2}{\Delta t} - \frac{2}{\Delta x^{2}} \quad\Longrightarrow\quad \Delta t_{\mathrm{max}} = \frac{\Delta x^2}{1 + |V_0| \Delta x^2 / 2}
$$
