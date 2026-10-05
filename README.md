# NEXUS-SCIENTIFIC-COMPUTING-ENGINE
NEXUS SCIENTIFIC COMPUTING ENGINE v1.0.0 # Moteur de calcul scientifique : omega, algebre, calcul, stats, physique, # theorie des nombres, Fourier, EDO. API REST + UI locale. # Auteur : Aissa Mohammedi (DGK) # Licence : NEXUS-OPEN-2.0 # Compatible a-Shell iOS - os.path uniquement - stdlib pure
```markdown<p align="center">
<img src="assets/banner.svg" alt="NEXUS Scientific Computing Engine" width="900">
</p>

<h1 align="center">NEXUS Scientific Computing Engine</h1>

<p align="center">
<strong>A complete scientific computing engine in pure Python stdlib.</strong><br>
<em>Special functions · Linear algebra · Calculus · Statistics · Number theory · Fourier · Physics.</em>
</p>

<p align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/License-NEXUS--OPEN--2.0-blue.svg" alt="License"></a>
<a href="#"><img src="https://img.shields.io/badge/version-1.0.0-brightgreen.svg" alt="Version"></a>
<a href="#"><img src="https://img.shields.io/badge/python-3.8%2B-blue.svg" alt="Python"></a>
<a href="#"><img src="https://img.shields.io/badge/dependencies-stdlib%20only-success.svg" alt="Zero deps"></a>
<a href="#"><img src="https://img.shields.io/badge/platform-linux%20%7C%20macos%20%7C%20ios%20(a--Shell)-lightgrey.svg" alt="Platform"></a>
<a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome"></a>
</p>

<p align="center">
<img src="assets/demo.gif" alt="NEXUS Science demo" width="800">
</p>

---

## The idea in one paragraph

Scientific Python normally means installing **NumPy, SciPy, SymPy, Pandas, Matplotlib** — over 500 MB of compiled dependencies that break on embedded systems, mobile devices, and air-gapped machines. NEXUS Scientific Computing Engine does the opposite: **one Python file, zero dependencies, full scientific toolkit.** It runs on a laptop, a phone, a Raspberry Pi, or a shell on iOS. It gives you the Omega constant, Lambert W, Riemann zeta, the Gamma function, Bessel functions, matrix algebra, calculus, statistics, number theory, Fourier transforms, and physics — all with pure Python 3.8+.

---

## Mathematical foundations

Every function in this engine is grounded in a named mathematical result. No magic, no black boxes.

### Ω — The Omega constant

The Omega constant is the unique real solution to

$$
x \, e^x = 1
$$

It is also defined as `W(1)`, where `W` is the Lambert W function:

$$
\Omega = W(1) \approx 0.5671432904097838729999686622\ldots
$$

Computed in this engine by fixed-point iteration on the transcendental equation:

$$
x_{n+1} = e^{-x_n}
$$

which converges quadratically in the neighborhood of Ω.

### W — The Lambert W function

Defined implicitly by

$$
W(x) \, e^{W(x)} = x
$$

Two real branches are supported:

| Branch | Domain |
|--------|--------|
| `W₀` | $x \ge -1/e$ |
| `W₋₁` | $-1/e \le x < 0$ |

Computed by **Halley's method**, a cubically convergent variant of Newton-Raphson:

$$
w_{n+1} = w_n - \frac{f(w_n)}{f'(w_n) - \dfrac{f(w_n) \cdot f''(w_n)}{2 \, f'(w_n)}}
\quad \text{with} \quad f(w) = w e^w - x
$$

### ζ — The Riemann zeta function

For $s > 1$:

$$
\zeta(s) = \sum_{k=1}^{\infty} \frac{1}{k^s}
$$

Computed by direct summation with N = 200 000 terms. For $s < 1$, the analytic continuation via the reflection formula is applied:

$$
\zeta(s) = 2^s \pi^{s-1} \sin\!\left(\frac{\pi s}{2}\right) \Gamma(1-s) \, \zeta(1-s)
$$

### Γ — The Gamma function

Extension of the factorial to the complex plane. Satisfies $\Gamma(n) = (n-1)!$ for positive integers.

Computed via the **Lanczos approximation** with $g = 7$ and 9 coefficients:

$$
\Gamma(z) \approx \sqrt{2\pi} \, (z+g-0.5)^{z-0.5} \, e^{-(z+g-0.5)} \, A_g(z)
$$

For negative $z$, the reflection formula is used:

$$
\Gamma(z) \Gamma(1-z) = \frac{\pi}{\sin(\pi z)}
$$

### B — The Beta function

$$
B(a,b) = \int_0^1 t^{a-1}(1-t)^{b-1} \, dt = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}
$$

### J₀, J₁ — Bessel functions of the first kind

Solutions to Bessel's differential equation:

$$
x^2 y'' + x y' + (x^2 - n^2) y = 0
$$

Computed via the power series:

$$
J_n(x) = \sum_{k=0}^{\infty} \frac{(-1)^k}{k! \, \Gamma(k+n+1)} \left(\frac{x}{2}\right)^{2k+n}
$$

### Ai — The Airy function

Solution to the Airy differential equation:

$$
y'' - x y = 0
$$

Computed via the Taylor series near the origin.

---

### Linear algebra

| Operation | Method | Complexity |
|-----------|--------|------------|
| Matrix multiplication | Direct triple loop | $O(n^3)$ |
| Determinant | Gaussian elimination with partial pivoting | $O(n^3)$ |
| Matrix inverse | Gauss-Jordan | $O(n^3)$ |
| Linear system `Ax = b` | Gaussian elimination | $O(n^3)$ |
| Matrix power `A^p` | Binary exponentiation | $O(\log p \cdot n^3)$ |
| Frobenius norm | Direct | $O(n^2)$ |

### Calculus

| Operation | Formula |
|-----------|---------|
| First derivative | $f'(x) \approx \dfrac{f(x+h) - f(x-h)}{2h}$ |
| Second derivative | $f''(x) \approx \dfrac{f(x+h) - 2f(x) + f(x-h)}{h^2}$ |
| Simpson's rule | $\displaystyle\int_a^b f \approx \frac{h}{3}\left[f(a) + 4\sum_{\text{odd}} + 2\sum_{\text{even}} + f(b)\right]$ |
| Trapezoid rule | $\displaystyle\int_a^b f \approx h \left[\frac{f(a) + f(b)}{2} + \sum_{i=1}^{n-1} f(a+ih)\right]$ |
| Newton-Raphson | $x_{n+1} = x_n - \dfrac{f(x_n)}{f'(x_n)}$ |
| Bisection | Iterative halving of $[a, b]$ where $f(a) \cdot f(b) < 0$ |

### Statistics

| Quantity | Formula |
|----------|---------|
| Mean | $\bar{x} = \dfrac{1}{n}\sum x_i$ |
| Variance (population) | $\sigma^2 = \dfrac{1}{n}\sum (x_i - \bar{x})^2$ |
| Variance (sample) | $s^2 = \dfrac{1}{n-1}\sum (x_i - \bar{x})^2$ |
| Pearson correlation | $r = \dfrac{\text{cov}(X,Y)}{\sigma_X \sigma_Y}$ |
| Linear regression | $y = a x + b$ where $a = \dfrac{\text{cov}(X,Y)}{\sigma_X^2}$ |
| Percentile (linear) | $p_k = s_{f} + (s_{c} - s_{f})(k - f)$ |

### Number theory

| Operation | Algorithm | Complexity |
|-----------|-----------|------------|
| Primality | Trial division up to $\sqrt{n}$ | $O(\sqrt{n})$ |
| Sieve of Eratosthenes | Classic sieve | $O(n \log \log n)$ |
| Prime factorization | Trial division | $O(\sqrt{n})$ |
| GCD | Euclidean algorithm | $O(\log \min(a,b))$ |
| Euler totient | Factorization-based | $O(\sqrt{n})$ |
| Partition function | Euler's pentagonal recurrence | $O(n \sqrt{n})$ |

### Fourier

| Transform | Formula |
|-----------|---------|
| DFT | $X_k = \sum_{n=0}^{N-1} x_n e^{-2\pi i k n / N}$ |
| IDFT | $x_n = \dfrac{1}{N} \sum_{k=0}^{N-1} X_k e^{2\pi i k n / N}$ |
| FFT | Recursive radix-2 Cooley-Tukey, $N = 2^k$ |

### Physics

| Quantity | Formula |
|----------|---------|
| Kinetic energy | $E_c = \tfrac{1}{2} m v^2$ |
| Potential energy | $E_p = m g h$ |
| Gravitational force | $F = G \dfrac{m_1 m_2}{r^2}$ |
| Electric force | $F = k \dfrac{q_1 q_2}{r^2}$ |
| Mass-energy | $E = m c^2$ |
| Lorentz factor | $\gamma = \dfrac{1}{\sqrt{1 - v^2 / c^2}}$ |
| Circular orbit velocity | $v = \sqrt{\dfrac{GM}{r}}$ |

---

## Architecture

<p align="center">
<img src="assets/architecture.svg" alt="Architecture" width="900">
</p>

```

nexus_science.py
├── Constants
├── Special functions
├── Linear algebra
├── Calculus
├── Statistics
├── Number theory
├── Fourier
├── Physics
├── Safe expression parser
├── HTTP dispatchers
├── Web server (ThreadingMixIn)
└── Main entry with port auto-detection

```

---

## Quick start

```bash
# Download the single file
curl -O https://raw.githubusercontent.com/Aissamohammedi88/nexus-science/main/nexus_science.py

# Run it
python3 nexus_science.py

# Open the browser
# → http://localhost:8920/
```

No pip install. No virtual environment. No compiled extensions.

---

Web interface

<p align="center">
<img src="assets/screenshot-ui.png" alt="Web interface" width="800">
</p>Eight tabs, each dedicated to one mathematical domain:

Tab Purpose
Omega Special functions (Lambert W, zeta, Gamma, Bessel…)
Algebra Matrix operations with JSON input
Calculus Derivatives, integrals, root-finding
Stats Descriptive stats, correlation, regression
Numbers Primality, factorization, totient, partitions
Fourier DFT, FFT, IDFT
Physics Energy, forces, relativity
Constants Full list of mathematical and physical constants

---

REST API

Every calculation is an HTTP endpoint.

Python

```python
import requests

r = requests.post("http://localhost:8920/api/omega", json={"fn": "omega"})
print(r.json()["resultat"]) # 0.5671432904097838
```

Bash

```bash
curl -X POST http://localhost:8920/api/linalg \
-H "Content-Type: application/json" \
-d '{"fn":"det","A":"[[1,2],[3,4]]"}'
```

JavaScript

```javascript
const r = await fetch("http://localhost:8920/api/fourier", {
method: "POST",
headers: { "Content-Type": "application/json" },
body: JSON.stringify({ fn: "fft", data: "1,1,1,1,0,0,0,0" })
});
const data = await r.json();
console.log(data.modules);
```

Full API surface

Endpoint Method Purpose
/api/omega POST Omega, Lambert W, zeta, Gamma, Beta, Bessel, Airy
/api/linalg POST Determinant, inverse, solve, transpose, trace
/api/calcul POST Derivative, integral, root-finding, limits
/api/stats POST Descriptive stats, correlation, regression
/api/nombres POST Primality, factorization, totient, partitions
/api/fourier POST DFT, FFT, IDFT
/api/phys ✅ique POST Energy, forces, relativity

`/ api/constantes` GET

---

Example outputs

Omega on constant

```
$ curl -s -X POST air http://localhost:8920/api/omega -d '{"fn":"omega"}' | jq
{
"ok": true,
"resultat": 0.5671432904097838,
"constante_officielle": 0.5671432904097838
}
```

Riemann zeta at s = 3

```
$ curl -s -X POST http://localhost:8920/api/omega -d '{"fn":"zeta","a":"3"}' | jq
{
"ok": true,
"resultat": 1.2020569031095943
}
```

Comparison with Apéry's constant: 1.2020569031595943. Error < 5·10⁻¹¹.

Determinant of a 2×2 matrix

```
$ curl -s -X POST http://localhost:8920/api/linalg \
-d '{"fn":"det","A":"[[1,2],[3,4]]"}' | jq
{
"ok": true,
"resultat": -2.0
}
```

FFT of a square pulse

```
$ curl -s -X POST http://localhost:8920/api/fourier \
-d '{"fn":"fft","data":"1,1,1,1,0,0,0,0"}' | jq
{
"ok": true,
"N": 8,
"modules": [4, 2.613, 0, 1.082, 0, 1.082, 0, 2.613]
}
```

The Fourier transform of a square pulse is the sinc-like pattern visible in modules.

Partition function p(100)

```
$ curl -s -X POST http://localhost:8920/api/nombres \
-d '{"fn":"part","n":"100"}' | jq
{
"ok": true,
"resultat": 190569292
}
```

Verifies the famous value: p(100) = 190 569 292.

---

Comparison with SciPy / NumPy

Feature SciPy / NumPy NEXUS Science
Install size ~500 MB ~50 KB
Dependencies C/Fortran compiled None
Works on iOS a-Shell ❌ -gapped systems
Works on Raspberry Pi Zero ⚠️ ✅
Ships with REST API ❌ ✅
Ships with web UI ❌ ✅
Every formula readable ❌ ✅
Handles matrices > 1000×1000 ✅ ⚠️ (O(n³) pure Python)
Eigenvalues ✅ ❌ (roadmap)
SVD ✅ ❌ (roadmap)
Stiff ODE solvers ✅ ❌

This tool is not a scipy replacement at scale. It is a self-contained scientific toolkit for constrained environments.

---

What is inside the code

<details>
<summary><b>Special functions</b></summary>· omega_constant_iter() — Omega constant via fixed-point
· lambert_w(x, branch) — Lambert W via Halley's method
· zeta_approx(s, terms) — Riemann zeta with reflection
· gamma_lanczos(z) — Gamma via Lanczos
· beta_function(a, b) — Beta from Gamma
· digamma_approx(x) — Digamma via log-Gamma
· bessel_j0(x), bessel_j1(x) — Bessel series
· airy_ai(x) — Airy via Taylor series

</details><details>
<summary><b>Linear algebra</b></summary>· mat_dot(A, B) — Matrix multiply
· mat_transpose(A)
· mat_identity(n)
· mat_det(A) — Gaussian elimination with pivot
· mat_inverse(A) — Gauss-Jordan
· mat_solve(A, b) — Linear system
· mat_power(A, p) — Binary exponentiation
· mat_trace(A)
· mat_norm_fro(A)

</details><details>
<summary><b>Calculus</b></summary>· derivee(f, x, h), derivee_seconde(f, x, h)
· integrale_simpson(f, a, b, n)
· integrale_trapeze(f, a, b, n)
· integrale_gauss(f, a, b)
· newton_raphson(f, df, x0)
· bissection(f, a, b)
· limite(f, x0, direction)

</details><details>
<summary><b>Statistics</b></summary>· stats_descriptives(xs)
· covariance(xs, ys)
· correlation(xs, ys)
· regression_lineaire(xs, ys)
· percentile(xs, p)
· combinaison(n, k), arrangement(n, k)

</details><details>
<summary><b>Number theory</b></summary>· est_premier(n)
· crible_eratosthene(n)
· factorisation(n)
· pgcd(a, b), ppcm(a, b)
· totiente_euler(n)
· partition_count(n)

</details><details>
<summary><b>Fourier</b></summary>· dft(xs), idft(Xs)
· fft(xs) — radix-2

</details><details>
<summary><b>Physics</b></summary>· energie_cinetique(m, v)
· energie_potentielle(m, g, h)
· force_gravitation(m1, m2, r)
· force_electrique(q1, q2, r)
· einstein_energie(m)
· lorentz_factor(v)
· orbite_circulaire(M, r)

</details>---

Why pure Python

Three reasons.

1. Portability. The engine runs anywhere Python 3.8+ runs. That includes a-Shell on iOS, Termux on Android, air-gapped Linux servers, embedded Linux devices, and educational environments where users cannot install compiled dependencies.

2. Transparency. Every formula is readable in the source. A student can open the file and see exactly what lambert_w(1) does, line by line. There is no compiled C to trust blindly.

3. Reproducibility. No version drift, no wheel mismatch, no ABI incompatibilities. The same file produces the same results on every machine, forever.

---

Security and privacy

· Server binds only to 127.0.0.1 — never exposed to the network.
· Expression parser uses eval with __builtins__ disabled and a whitelist of allowed functions.
· No file writes outside ~/Documents/nexus_science.
· No network calls. No telemetry. No tracking.
· Fully offline after the initial download.

---

Roadmap

□ Eigenvalues and eigenvectors (QR algorithm)
□ Singular value decomposition (one-sided Jacobi)
□ Adaptive Simpson integration
□ Complex number support in the expression parser
□ Save/load results to disk (JSON)
□ Export to CSV and LaTeX
□ SVG plotting (no matplotlib)
□ Erf, Bessel Y, Hankel, Struve functions
□ WebAssembly build for browser-only use

---

Contributing

See CONTRIBUTING.md.

Quick rules:

1. Zero external dependencies (stdlib only)
2. Python 3.8+ compatibility
3. Every function documented with its formula
4. Tests for every new function
5. No unsafe eval

---

License

NEXUS-OPEN-2.0 — see LICENSE.

---

Author

Aissa Mohammedi (DGK)
Systems Architect · Quebec, Canada

· GitHub: @Aissamohammedi88
· LinkedIn: linkedin.com/in/aissa-mohammedi-2308743b2

---

<p align="center">
<strong>NEXUS Scientific Computing Engine</strong><br>
<em>Full scientific toolbox. One file. Zero dependencies.</em><br>
<sub>Built by Aissa Mohammedi (DGK) — NEXUS-OPEN-2.0</sub>
</p><p align="center">
<img src="assets/omega.svg" alt="Omega constant" width="80">
<img src="assets/zeta.svg" alt="Riemann zeta" width="80">
<img src="assets/fourier.svg" alt="Fourier" width="80">
<img src="assets/matrix.svg" alt="Matrix" width="80">
<img src="assets/atom.svg" alt="Physics" width="80">
</p>
````---

Les images à créer pour ce README

Le README référence 7 images dans le dossier assets/. Voici comment les créer.

1. assets/banner.svg — Bannière principale

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 200" width="900" height="200">
<defs>
<linearGradient id="g1" x1="0%" y1="0%" x2="100%" y2="100%">
<stop offset="0%" style="stop-color:#fff"/>
<stop offset="40%" style="stop-color:#00d4ff"/>
<stop offset="70%" style="stop-color:#a855f7"/>
<stop offset="100%" style="stop-color:#ff6ec7"/>
</linearGradient>
<radialGradient id="bg" cx="50%" cy="50%" r="80%">
<stop offset="0%" style="stop-color:#0a1018"/>
<stop offset="100%" style="stop-color:#000"/>
</radialGradient>
</defs>
<rect width="900" height="200" fill="url(#bg)"/>
<text x="450" y="90" text-anchor="middle" font-family="-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,sans-serif" font-size="56" font-weight="800" fill="url(#g1)" letter-spacing="-2">
NEXUS SCIENCE
</text>
<text x="450" y="130" text-anchor="middle" font-family="-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,sans-serif" font-size="16" font-weight="400" fill="#6a7a8a" letter-spacing="4">
SCIENTIFIC COMPUTING ENGINE
</text>
<text x="450" y="165" text-anchor="middle" font-family="ui-monospace,monospace" font-size="12" fill="#00d4ff" letter-spacing="2">
Ω · ζ · Γ · W · J · FFT · EDO · π
</text>
</svg>
```

2. assets/omega.svg — Symbole Ω

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
<circle cx="50" cy="50" r="45" fill="none" stroke="#00d4ff" stroke-width="2"/>
<text x="50" y="68" text-anchor="middle" font-family="serif" font-size="52" fill="#00d4ff" font-style="italic">Ω</text>
</svg>
```

3. assets/zeta.svg — Symbole ζ

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
<circle cx="50" cy="50" r="45" fill="none" stroke="#a855f7" stroke-width="2"/>
<text x="50" y="68" text-anchor="middle" font-family="serif" font-size="52" fill="#a855f7" font-style="italic">ζ</text>
</svg>
```

4. assets/fourier.svg — Symbole Fourier

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
<circle cx="50" cy="50" r="45" fill="none" stroke="#ff6ec7" stroke-width="2"/>
<path d="M 20 60 Q 35 20, 50 50 T 80 40" fill="none" stroke="#ff6ec7" stroke-width="2"/>
<text x="50" y="80" text-anchor="middle" font-family="serif" font-size="20" fill="#ff6ec7">∿</text>
</svg>
```

5. assets/matrix.svg — Symbole Matrix

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
<rect x="5" y="5" width="90" height="90" fill="none" stroke="#4ade80" stroke-width="2" rx="45"/>
<text x="50" y="65" text-anchor="middle" font-family="ui-monospace,monospace" font-size="36" fill="#4ade80">[A]</text>
</svg>
```

6. assets/atom.svg — Symbole physique

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
<circle cx="50" cy="50" r="45" fill="none" stroke="#fbbf24" stroke-width="2"/>
<circle cx="50" cy="50" r="5" fill="#fbbf24"/>
<ellipse cx="50" cy="50" rx="40" ry="15" fill="none" stroke="#fbbf24" stroke-width="1.5" opacity="0.6"/>
<ellipse cx="50" cy="50" rx="40" ry="15" fill="none" stroke="#fbbf24" stroke-width="1.5" opacity="0.6" transform="rotate(60 50 50)"/>
<ellipse cx="50" cy="50" rx="40" ry="15" fill="none" stroke="#fbbf24" stroke-width="1.5" opacity="0.6" transform="rotate(120 50 50)"/>
</svg>
```

7. assets/architecture.svg — Schéma d'architecture

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 500" width="900" height="500">
<rect width="900" height="500" fill="#050810"/>

<style>
.box { fill: #0a1018; stroke: #1a2540; stroke-width: 2; rx: 8; }
.title { font-family: -apple-system, sans-serif; font-size: 14px; font-weight: 700; fill: #00d4ff; text-anchor: middle; }
.sub { font-family: ui-monospace, monospace; font-size: 10px; fill: #6a7a8a; text-anchor: middle; }
.line { stroke: #00d4ff; stroke-width: 1.5; fill: none; opacity: 0.4; }
</style>

<text x="450" y="35" text-anchor="middle" font-family="sans-serif" font-size="20" font-weight="800" fill="#fff">
NEXUS Science — Architecture
</text>

<!-- Row 1: Special + Linear + Calculus -->
<rect class="box" x="30" y="70" width="260" height="90"/>
<text class="title" x="160" y="100">Special Functions</text>
<text class="sub" x="160" y="120">Ω · W · ζ · Γ · B · J · Ai</text>
<text class="sub" x="160" y="140">Lambert, Bessel, Airy</text>

<rect class="box" x="320" y="70" width="260" height="90"/>
<text class="title" x="450" y="100">Linear Algebra</text>
<text class="sub" x="450" y="120">det · inv · solve</text>
<text class="sub" x="450" y="140">Gauss · Gauss-Jordan</text>

<rect class="box" x="610" y="70" width="260" height="90"/>
<text class="title" x="740" y="100">Calculus</text>
<text class="sub" x="740" y="120">deriv · integ · root</text>
<text class="sub" x="740" y="140">Simpson · Newton · Bisect</text>

<!-- Row 2: Stats + Numbers + Fourier -->
<rect class="box" x="30" y="190" width="260" height="90"/>
<text class="title" x="160" y="220">Statistics</text>
<text class="sub" x="160" y="240">mean · var · corr · reg</text>
<text class="sub" x="160" y="260">Pearson · percentile</text>

<rect class="box" x="320" y="190" width="260" height="90"/>
<text class="title" x="450" y="220">Number Theory</text>
<text class="sub" x="450" y="240">prime · factor · φ · p(n)</text>
<text class="sub" x="450" y="260">Sieve · totient · partition</text>

<rect class="box" x="610" y="190" width="260" height="90"/>
<text class="title" x="740" y="220">Fourier</text>
<text class="sub" x="740" y="240">DFT · FFT · IDFT</text>
<text class="sub" x="740" y="260">Radix-2 Cooley-Tukey</text>

<!-- Middle layer: Parser + Dispatch -->
<rect class="box" x="230" y="310" width="440" height="60" style="stroke:#a855f7"/>
<text class="title" x="450" y="340" style="fill:#a855f7">Safe Expression Parser + Dispatchers</text>
<text class="sub" x="450" y="358">whitelist · __builtins__ disabled</text>

<!-- Bottom: HTTP Server -->
<rect class="box" x="280" y="400" width="340" height="60" style="stroke:#ff6ec7"/>
<text class="title" x="450" y="430" style="fill:#ff6ec7">HTTP Server · 127.0.0.1:8920</text>
<text class="sub" x="450" y="448">REST API + Web UI</text>

<!-- Arrows -->
<line class="line" x1="160" y1="160" x2="160" y2="190"/>
<line class="line" x1="450" y1="160" x2="450" y2="190"/>
<line class="line" x1="740" y1="160" x2="740" y2="190"/>

<line class="line" x1="160" y1="280" x2="230" y2="310"/>
<line class="line" x1="450" y1="280" x2="450" y2="310"/>
<line class="line" x1="740" y1="280" x2="670" y2="310"/>

<line class="line" x1="450" y1="370" x2="450" y2="400"/>
</svg>
```

8. assets/demo.gif et assets/screenshot-ui.png

Ces deux fichiers sont des captures d'écran réelles — pas des SVG. À faire :

Pour screenshot-ui.png :

1. Lance le script
2. Ouvre http://localhost:8920/ dans un navigateur
3. Prends une capture d'écran de l'interface (pleine page, onglet Omega visible)
4. Sauvegarde en PNG, largeur ~1600px
5. Place dans assets/screenshot-ui.png

Pour demo.gif :

1. Lance le script
2. Utilise un outil d'enregistrement (Peek sur Linux, Kap sur macOS, ScreenToGif sur Windows)
3. Enregistre 10 secondes : clic sur onglet Omega, clic sur Calculer, résultat qui apparaît
4. Export en GIF, max 800×500px, < 3 MB
5. Place dans assets/demo.gif

---

Structure finale du repo

```
nexus-science/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
├── .gitignore
├── .gitattributes
├── .editorconfig
├── nexus_science.py
├── assets/
│ ├── banner.svg
│ ├── architecture.svg
│ ├── omega.svg
│ ├── zeta.svg
│ ├── fourier.svg
│ ├── matrix.svg
│ ├── atom.svg
│ ├── screenshot-ui.png
│ └── demo.gif
├── docs/
├── examples/
├── tests/
└── .github/
└── workflows/
└── test.yml
```

---
