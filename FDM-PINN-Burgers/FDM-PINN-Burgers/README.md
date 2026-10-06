# FDM-PINN for the 1D Burgers Equation

Research project investigating **Finite-Difference Physics-Informed Neural Networks (FDM-PINNs)** for solving the 1D viscous Burgers equation.

## Research objective

This project studies whether finite-difference approximations can replace automatic differentiation (AD) for evaluating the PDE residual inside a Physics-Informed Neural Network.

The current benchmark compares:

- **AD-PINN** — derivatives obtained with PyTorch automatic differentiation.
- **FDM-PINN** — derivatives obtained using central finite-difference stencils.

The current experiments also investigate the effect of the finite-difference step size `h`.

## PDE

The 1D viscous Burgers equation is

\[
u_t + u u_x - \nu u_{xx} = 0,
\]

with

\[
\nu = \frac{0.01}{\pi},
\]

on

\[
x \in [-1,1], \qquad t \in [0,1].
\]

Initial condition:

\[
u(x,0)=-\sin(\pi x)
\]

and homogeneous boundary conditions:

\[
u(-1,t)=u(1,t)=0.
\]

## Neural network

The current implementation uses a fully connected MLP:

- Input: `(x, t)`
- Four hidden layers
- 50 neurons per hidden layer
- `Tanh` activation
- Output: `u(x,t)`

## Current experiments

### AD-PINN baseline

The current notebook trains the AD-PINN for 10,000 Adam iterations with learning rate `1e-3`.

| Metric | Current result |
|---|---:|
| Epochs | 10,000 |
| Training time | 242.59 s |
| Final total loss | 6.888920e-04 |
| Relative L2 error | 3.631237e-02 |

The reference solution is generated independently and is not used to train the PINN.

### FDM step-size study

The current FDM experiments train each model for 5,000 iterations.

| h | Relative L2 Error | PDE Residual MSE | Time (s) |
|---:|---:|---:|---:|
| 1e-1 | 4.366016e-01 | 1.775516e-02 | 74.17 |
| 1e-2 | 1.992037e-01 | 1.247763e-02 | 54.23 |
| 1e-3 | 2.291760e-01 | 1.041085e-02 | 51.50 |

### Important interpretation

These numbers are **current research results, not final conclusions**.

The AD-PINN baseline uses 10,000 epochs, while the FDM step-size experiments use 5,000 epochs. Therefore, their training times should **not** be interpreted as a controlled speed comparison yet.

The next controlled experiment should use the same architecture, optimizer, learning rate, number of epochs, collocation strategy, and evaluation protocol for AD-PINN and FDM-PINN.

## Repository structure

```text
FDM-PINN-Burgers/
├── notebooks/
│   └── 01_FDM_PINN_Burgers.ipynb
├── results/
│   └── current_results.md
├── figures/
├── archive/
│   └── original Jupyter HTML export
├── README.md
├── requirements.txt
└── .gitignore
```

## Installation

```bash
pip install -r requirements.txt
```

Recommended environment:

- Python 3.x
- PyTorch
- NumPy
- SciPy
- Matplotlib
- Jupyter

## Running the experiment

Open:

```text
notebooks/01_FDM_PINN_Burgers.ipynb
```

and run the cells sequentially.

The code automatically uses CUDA when a compatible GPU is available.

## Status

**Research in progress.**

Current focus:

1. Establish a controlled AD-PINN baseline.
2. Establish a controlled FDM-PINN baseline.
3. Study finite-difference step-size sensitivity.
4. Compare accuracy, PDE residual, convergence, and computational cost.
5. Investigate further numerical-analysis and verification directions.

## Author

**Saurabh Singh**

Dual Degree B.Tech + M.Tech, Computer Science  
South Asian University, New Delhi
