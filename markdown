# NEXUS SCIENTIFIC COMPUTING ENGINE
[![License: NEXUS-OPEN-2.0](https://img.shields.io/badge/License-NEXUS--OPEN--2.0-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen.svg)]()
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)]()
[![Platform](https://img.shields.io/badge/platform-linux%20%7C%20macos%20%7C%20ios%20(a--Shell)-lightgrey.svg)]()
[![Zero deps](https://img.shields.io/badge/dependencies-stdlib%20only-success.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

> **A complete scientific computing engine in pure Python stdlib. Special functions, linear algebra, calculus, statistics, number theory, Fourier, physics. Local web UI + REST API. Zero dependencies.**

NEXUS Scientific Computing Engine is a single-file Python tool that gives you a full scientific toolbox without `scipy`, without `numpy`, without `sympy`. Just Python 3.8+ and the standard library.

Author: **Aissa Mohammedi (DGK)**
License: **NEXUS-OPEN-2.0**
Version: **1.0.0**

---

## Why this project exists

Scientific Python normally means:

```
pip install numpy scipy sympy pandas matplotlib
```

That's 500 MB of dependencies. Compiled C extensions. Version conflicts. Wheels that don't exist for your architecture.

**NEXUS Scientific Computing Engine does it differently:**

- One file. Zero dependencies. Pure stdlib.
- Works on a-Shell iOS, on Linux, on macOS, on any Python 3.8+.
- Full REST API so you can call it from any language.
- Full local web UI so you can use it without writing code.
- Educational transparency — every formula is readable.

It is not a replacement for scipy at scale. It is a **self-contained scientific toolkit** for anywhere scipy cannot be installed, or for anyone who wants to understand what is happening under the hood.

---

## What's inside

| Domain | Functions |
|--------|-----------|
| **Special functions** | Omega constant, Lambert W (both branches), Riemann zeta, Gamma (Lanczos), Beta, Digamma, Bessel J0/J1, Airy Ai |
| **Linear algebra** | Matrix multiplication, transpose, identity, determinant, inverse, linear solve (Gauss), matrix power, trace, Frobenius norm |
| **Calculus** | Numerical derivative (1st, 2nd), Simpson integration, Trapezoid integration, Gauss-Legendre quadrature, Newton-Raphson, Bisection, limits |
| **Statistics** | Descriptive stats, covariance, Pearson correlation, linear regression, percentiles, combinations, permutations |
| **Number theory** | Primality test, Sieve of Eratosthenes, prime factorization, Euler totient, partition function p(n), GCD, LCM |
| **Fourier** | DFT (direct), FFT (radix-2), inverse DFT |
| **Physics** | Kinetic energy, potential energy, gravitational force, electric force, mass-energy equivalence, Lorentz factor, circular orbit velocity |
| **Constants** | π, e, φ, γ, Ω, Catalan, Apéry, Khinchin, Glaisher, Feigenbaum δ and α, c, G, h, e⁻ |

---

## Quick start

```bash
# Download
curl -O https://raw.githubusercontent.com/Aissamohammedi88/nexus-science/main/nexus_science.py

# Run
python3 nexus_science.py

# Open the browser
# → http://localhost:8920/
```

No installation. No dependencies.

---

## Web interface

Eight tabs, each with a dedicated calculator:

| Tab | Purpose |
|-----|---------|
| **Omega** | Special functions with input for arguments |
| **Algebra** | Matrix operations with JSON input |
| **Calculus** | Derivatives, integrals, root-finding on user expressions |
| **Stats** | Descriptive stats, correlation, regression |
| **Numbers** | Primality, factorization, totient, partitions |
| **Fourier** | DFT, FFT, IDFT on signal vectors |
| **Physics** | Energy, forces, relativity |
| **Constants** | Full list of mathematical and physical constants |

---

## REST API

Every calculation is available as an HTTP endpoint.

### Special functions

```bash
curl -X POST http://localhost:8920/api/omega \
-H "Content-Type: application/json" \
-d '{"fn": "omega"}'
```

```json
{ "ok": true, "resultat": 0.5671432904097838, "constante_officielle": 0.5671432904097838 }
```

```bash
# Lambert W
curl -X POST http://localhost:8920/api/omega \
-d '{"fn": "lambert", "a": "1"}'
```

```bash
# Riemann zeta
curl -X POST http://localhost:8920/api/omega \
-d '{"fn": "zeta", "a": "3"}'
```

```bash
# Gamma
curl -X POST http://localhost:8920/api/omega \
-d '{"fn": "gamma", "a": "5.5"}'
```

### Linear algebra

```bash
curl -X POST http://localhost:8920/api/linalg \
-d '{"fn": "det", "A": "[[1,2],[3,4]]"}'
```

```bash
curl -X POST http://localhost:8920/api/linalg \
-d '{"fn": "solve", "A": "[[2,1],[1,3]]", "b": "[5,10]"}'
```

### Calculus

```bash
curl -X POST http://localhost:8920/api/calcul \
-d '{"fn": "deriv", "expr": "x**2 + 3*x - 1", "a": "2"}'
```

```bash
curl -X POST http://localhost:8920/api/calcul \
-d '{"fn": "integ_simpson", "expr": "sin(x)", "a": "0", "b": "3.14159"}'
```

### Statistics

```bash
curl -X POST http://localhost:8920/api/stats \
-d '{"fn": "desc", "data": "1,2,3,4,5,6,7,8,9,10"}'
```

```bash
curl -X POST http://localhost:8920/api/stats \
-d '{"fn": "reg", "data": "1,2,3,4,5", "data2": "2,4,6,8,11"}'
```

### Number theory

```bash
curl -X POST http://localhost:8920/api/nombres \
-d '{"fn": "fact", "n": "123456789"}'
```

```bash
curl -X POST http://localhost:8920/api/nombres \
-d '{"fn": "part", "n": "100"}'
```

### Fourier

```bash
curl -X POST http://localhost:8920/api/fourier \
-d '{"fn": "fft", "data": "1,1,1,1,0,0,0,0"}'
```

### Physics

```bash
curl -X POST http://localhost:8920/api/physique \
-d '{"fn": "einstein", "a": "1"}'
```

```bash
curl -X POST http://localhost:8920/api/physique \
-d '{"fn": "orbite", "a": "5.972e24", "b": "6.371e6"}'
```

---

## Technical details

### Omega constant

The Omega constant is the unique real solution to `x·e^x = 1`. It equals `W(1)` where `W` is the Lambert W function.

Computed by fixed-point iteration: `x_{n+1} = e^{-x_n}`.

```
Ω = 0.5671432904097838729999686622...
```

### Lambert W

Two branches supported:

- **W₀** (main branch, `x ≥ -1/e`)
- **W₋₁** (lower branch, `-1/e ≤ x < 0`)

Computed via Halley's method with quadratic convergence:

```
w_{n+1} = w_n - f(w_n) / (f'(w_n) - f(w_n)·f''(w_n) / (2·f'(w_n)))
```

where `f(w) = w·e^w - x`.

### Gamma function

Lanczos approximation with g=7 and 9 coefficients, giving ~15 digits of accuracy for real arguments.

### Riemann zeta

Direct summation `Σ 1/k^s` for `s > 1`, with reflection formula for `s < 1`.

### FFT

Radix-2 Cooley-Tukey. Requires N to be a power of 2.

### Expression parser

Safe expression evaluator. Only whitelisted functions and constants are exposed. `eval` runs with `__builtins__` disabled.

Supported syntax:

```
x**2 + 3*x - 1
sin(x), cos(x), tan(x), asin, acos, atan
sinh, cosh, tanh, exp, log, log10, sqrt
abs, floor, ceil, sign
pi, e, phi, omega, gamma, catalan
```

---

## Architecture

```
nexus_science.py
├── Constants
│ ├── PI, E, PHI, GAMMA_EULER
│ ├── OMEGA_CONST, CATALAN, APERY
│ └── FEIGENBAUM_D, FEIGENBAUM_A
│
├── Special functions
│ ├── omega_constant_iter()
│ ├── lambert_w()
│ ├── zeta_approx()
│ ├── gamma_lanczos()
│ ├── beta_function()
│ ├── digamma_approx()
│ ├── bessel_j0(), bessel_j1()
│ └── airy_ai()
│
├── Linear algebra
│ ├── mat_dot(), mat_transpose()
│ ├── mat_identity(), mat_det()
│ ├── mat_inverse(), mat_solve()
│ ├── mat_power()
│ ├── mat_trace(), mat_norm_fro()
│
├── Calculus
│ ├── derivee(), derivee_seconde()
│ ├── integrale_simpson()
│ ├── integrale_trapeze()
│ ├── integrale_gauss()
│ ├── newton_raphson()
│ ├── bissection()
│ └── limite()
│
├── Statistics
│ ├── stats_descriptives()
│ ├── covariance(), correlation()
│ ├── regression_lineaire()
│ ├── percentile()
│ ├── combinaison(), arrangement()
│
├── Number theory
│ ├── est_premier()
│ ├── crible_eratosthene()
│ ├── factorisation()
│ ├── pgcd(), ppcm()
│ ├── totiente_euler()
│ └── partition_count()
│
├── Fourier
│ ├── dft(), idft()
│ └── fft()
│
├── Physics
│ ├── energie_cinetique()
│ ├── energie_potentielle()
│ ├── force_gravitation()
│ ├── force_electrique()
│ ├── einstein_energie()
│ ├── lorentz_factor()
│ └── orbite_circulaire()
│
├── Parser
│ ├── parser_expr() — safe eval
│ ├── parser_liste() — "1,2,3" → [1,2,3]
│ └── parser_matrice() — JSON matrix
│
├── Dispatch
│ ├── dispatch_omega()
│ ├── dispatch_linalg()
│ ├── dispatch_calcul()
│ ├── dispatch_stats()
│ ├── dispatch_nombres()
│ ├── dispatch_fourier()
│ └── dispatch_physique()
│
├── HTTP
│ ├── Handler
│ └── Server (ThreadingMixIn)
│
└── Main
└── Auto port detection + startup banner
```

---

## Files generated

```
~/Documents/nexus_science/
├── logs/
│ └── science.log
└── results/
└── (future: saved results)
```

Nothing is written outside this folder.

---

## Security

- **Localhost only** — the HTTP server binds to `127.0.0.1`
- **Safe eval** — user expressions are evaluated with `__builtins__` disabled and only whitelisted functions exposed
- **No file writes** outside `~/Documents/nexus_science`
- **No telemetry** — nothing leaves the machine
- **No network calls** — the engine is fully offline
- **Timeout protection** — zeta and FFT bounded by iteration limits

---

## Limitations (honest)

This tool is **not** a replacement for scipy at scale. Known limitations:

| Limitation | Detail |
|------------|--------|
| Riemann zeta | Only converges well for s > 1. Reflection formula is approximate for small s. |
| FFT | Only radix-2. N must be power of 2. |
| Bessel, Airy | Series only. Not accurate for large arguments. |
| Eigenvalues | Not implemented (would require QR or Lanczos) |
| SVD | Not implemented |
| ODE | Euler and RK4 only. No stiff solvers. |
| Integration | No adaptive quadrature. |
| Complex support | Partial (via cmath for Fourier) |

For production scientific work, use scipy. For everything else — teaching, embedded systems, mobile, offline environments, quick calculations — this works.

---

## Roadmap

- [ ] Eigenvalues via QR algorithm
- [ ] SVD via one-sided Jacobi
- [ ] Adaptive Simpson integration
- [ ] Complex number support in expression parser
- [ ] Save/load results to disk
- [ ] Export to CSV / LaTeX
- [ ] Plotting via SVG (no matplotlib)
- [ ] More special functions (Erf, Bessel Y, Hankel, Struve)
- [ ] WebAssembly build for browser-only use

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

Rules:

1. Zero external dependencies (stdlib only)
2. Python 3.8+ compatibility
3. Every new function has tests
4. No `eval` without `__builtins__` disabled
5. Document the mathematical formula used

---

## License

**NEXUS-OPEN-2.0** — see [LICENSE](LICENSE).

---

## Author

**Aissa Mohammedi (DGK)**
Systems Architect · Quebec, Canada

- GitHub: [@Aissamohammedi88](https://github.com/Aissamohammedi88)
- LinkedIn: [linkedin.com/in/aissa-mohammedi-2308743b2](https://linkedin.com/in/aissa-mohammedi-2308743b2)

---

## Acknowledgments

- Inspired by the pain of installing scipy on constrained systems
- Built for developers who want to understand what's under the hood
- Named in honor of the Omega constant, one of the most elegant numbers in mathematics

---

<p align="center">
<strong>NEXUS SCIENTIFIC COMPUTING ENGINE</strong><br>
<em>Full scientific toolbox. One file. Zero dependencies.</em><br>
<sub>Built by Aissa Mohammedi (DGK) — NEXUS-OPEN-2.0</sub>
</p>
