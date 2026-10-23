# PDEs-in-Simulating-Extended-Reality-Experiences

This project applies **Partial Differential Equations (PDEs)** to two core problems in Extended Reality (XR): how touch propagates through tissue (haptic feedback) and where a user looks in a scene (visual saliency and gaze prediction). It shows that both reduce to PDEs with physically motivated boundary conditions.

Institution: Zewail University, Faculty of Engineering  
Department: Communications and Information  
Date: May 2026  

---

## 🚀 Project Overview

The project consists of two case studies:

### 1️⃣ Part I – Haptic Feedback via Wave PDEs
- Wave propagation through a soft-tissue layer driven by a surface haptic actuator
- Domain `0 < x < L, t > 0` with identical boundary and initial conditions for all models
- Three progressive models
- Analytical solutions via Laplace transform and Cauchy residues
- Explicit finite-difference (FD) solvers validated against the analytical solutions

| Model | PDE | Behaviour |
|-------|-----|-----------|
| Model 1 – Classical Wave | `u_tt = c² u_xx` | Lossless standing wave, no decay |
| Model 2 – Modified Viscoelastic | `u_tt = c² u_xx + ν u_xxt` | Spatial attenuation, decaying transients |
| Model 3 – Shao (2022) Kelvin–Voigt | Same PDE as Model 2 | Travelling wave `A₀ e^(−αx) cos(ωt − k_r x)` |

📌 Concepts Demonstrated:
- Laplace transform and Bromwich integral
- Residue theorem for inverting the transform
- Kelvin–Voigt viscoelasticity
- Finite-difference schemes and the CFL stability condition
- Frequency-dependent attenuation and dispersion

---

### 2️⃣ Part II – Gaze Tracking and Visual Saliency
- Saliency framed as a boundary-value problem on the image
- Image split into superpixels, with content-aware edge weights `k(p,q) = exp(−β‖h(p) − h(q)‖²)`
- Laplace equation generalised to a weighted graph Laplacian (LESD)
- Convex-hull foreground/background split
- Guidance map built from three priors
- Greedy seed selection, then a final linear solve for the saliency map

Guidance map:

```
g(p) = f_f(p) × f_c(p) × f_l(p)
```

| Prior | Meaning |
|-------|---------|
| `f_f` Background diffusion | How isolated is the node from the background? |
| `f_c` Color | How different is its color from the background? |
| `f_l` Center | How close is it to the image center? |

📌 Concepts Demonstrated:
- Discretising the Laplace equation with finite differences
- Dirichlet boundary conditions
- Assembling and solving the sparse system `A f = b`
- Thresholding the saliency map into a masked region
- Tests on a synthetic VR scene and a real photograph

---

## 🔬 Key Results

| Result | Value |
|--------|-------|
| FD vs. analytical error, Model 1 | < 0.8% (relative L² error) |
| FD vs. analytical error, Model 2 | < 1.0% (relative L² error) |
| Model 2 steady state vs. Shao | Algebraically and numerically equivalent |
| Reduction to Model 1 | Setting `ν = 0` recovers the classical wave equation |

### 🛠 XR Design Insights

| Observation | Implication |
|-------------|-------------|
| High-frequency signals (f > 300 Hz) decay strongly | Effective penetration depth is under 2 cm |
| Low-frequency actuation (f < 100 Hz) travels deep | May excite persistent resonances |
| Saliency diffuses only across similar-color edges (`k ≈ 0` at object boundaries) | Saliency stays confined inside the object |

---

## 📚 References

- Shao, *Tactile Sensing, Information, and Feedback via Wave Propagation*, Springer, 2022
- Liu et al., *Adaptive Partial Differential Equation Learning for Visual Saliency Detection*, IEEE CVPR, 2014
- Zhao et al., *Learning Partial Differential Equations for Saliency Detection*, IEEE ICSP, 2016
- Zill & Wright, *Advanced Engineering Mathematics*
- Haberman, *Applied Partial Differential Equations*
- Walker et al., *VisualPDE: Rapid Interactive Simulations of Partial Differential Equations*, 2023

---

## 👨‍💻 Authors

- Mohamed Ali  
- Mohammed Soliman  

---

## 📌 Key Takeaway

This project shows that a single mathematical language, PDEs, covers both the physics of touch and the perception of sight in XR, using hyperbolic wave equations for haptics and elliptic graph-Laplacian systems for saliency.
