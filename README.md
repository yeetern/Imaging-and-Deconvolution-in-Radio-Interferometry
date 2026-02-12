# 📡 Imaging and Deconvolution in Radio Interferometry

> **Exploring radio interferometric imaging as an inverse problem:**
> How incomplete Fourier sampling maps to sky images, why this is *not* a simple inverse transform, and what assumptions drive different reconstruction approaches.

---

## 📘 Motivation

Radio interferometers — like the VLA, ALMA, and VLBI arrays — do not measure images directly. They sample the *Fourier domain (visibilities)*, capturing only a subset of spatial frequency information. Recovering a sky image from this incomplete and noisy data is a *fundamentally ill-posed inverse problem*.

This repository exists to bridge **physical intuition** with **computational experiments**, building understanding from first principles, and illuminating the assumptions behind different imaging strategies.

Primary references:

* 📑 Wilner (2014), *Imaging and Deconvolution* (NRAO Synthesis Imaging Workshop)
* 🎥 YouTube lecture on interferometric imaging theory

---

## 🎯 Learning Goals

By working through this repo, *you* should be able to:

1. **Explain what visibilities are** and how they relate to sky brightness via the van Cittert–Zernike theorem.
2. **Understand how incomplete (u,v) sampling creates “dirty images”** and why a simple inverse Fourier transform is inadequate.
3. **Evaluate different weighting schemes** (natural, uniform, Briggs/robust) and their effects on resolution and sensitivity.
4. **Interpret the CLEAN algorithm and its assumptions**, and articulate why deconvolution is fundamentally a choice of regularization / prior.
5. **Perform simple experiments** that reproduce these effects and quantify trade-offs.

---

## 🧠 Core Concepts (Summarized)

### 1. Visibilities & the Fourier Transform

* The interferometer measures complex visibilities — samples of the Fourier transform of the sky brightness distribution.
* Due to finite baselines, the sampling in (u,v) space is incomplete, leading to a *dirty beam* rather than a perfect delta function.

### 2. Dirty Image vs. True Sky

* Dirty image = inverse Fourier transform of sampled visibilities.
* The dirty beam’s sidelobes and missing frequencies cause artifacts and bias.
* Deconvolution is the process of *estimating* the true sky given this incomplete information.

### 3. Weighting & Imaging Trade-offs

Different ways to weight visibilities change the effective point spread function (PSF) and noise characteristics:

| Scheme        | Resolution | Sensitivity | Notes                     |
| ------------- | ---------- | ----------- | ------------------------- |
| Natural       | Lower      | Highest     | Good for diffuse emission |
| Uniform       | Higher     | Lower       | Suppresses PSF sidelobes  |
| Briggs/Robust | Tunable    | Balanced    | Adjustable trade-off      |

### 4. Inverse Problem & Assumptions

The central lesson:

> There are *infinitely many* sky brightness distributions that are consistent with the observed visibilities.

Any algorithm (CLEAN, MEM, Bayesian, sparse recovery) implicitly *chooses a prior assumption* about the sky.

---

## 📁 Repository Structure

```
/
├── README.md
├── LICENSE
├── 01_foundations/
│   ├── theory_visibilities.md
│   ├── van_cittert_zernike.md
│   ├── incomplete_sampling.md
├── 02_experiments/
│   ├── simulate_uv_coverage.py
│   ├── dirty_image_vs_true.ipynb
│   ├── weighting_comparison.ipynb
├── 03_deconvolution/
│   ├── clean_basics.md
│   ├── clean_vs_ms_clean.ipynb
│   ├── inversion_regularization_overview.md
├── 04_judgements/
│   ├── when_clean_fails.md
│   ├── artefacts_vs_signal.md
│   └── interpretation_checklist.md
└── references/
    ├── wilner_2014.pdf
    └── lecture_link.txt
```

---

## 🧪 Example Notebooks

These notebooks are designed to not only *show* results but *teach why* they happen:

✔ **dirty_image_vs_true.ipynb**
Compare a simulated visibility sampling with the corresponding dirty image and quantify how missing low spatial frequencies distort large-scale emission.

✔ **weighting_comparison.ipynb**
Apply natural, uniform, and robust weighting on the same uv distribution and visualize their effects on PSF and image quality.

✔ **clean_vs_ms_clean.ipynb**
Illustrate how scale-aware deconvolution handles extended emission differently from classic CLEAN.

---

## 🧭 How to Use This Repo

### 📌 Prerequisites

Python environment with:

```bash
numpy
matplotlib
astropy
scipy
jupyterlab
```

### 🚀 Running Experiments

1. Clone the repo.
2. Install dependencies.
3. Launch JupyterLab and explore notebooks in `02_experiments/` and `03_deconvolution/`.
4. Read the theory notes before executing code.

---

## 💡 What This Repo Is *Not*

❌ Not just “course notes”
❌ Not a black-box imaging software
❌ Not tied to a single tool (e.g., CASA)

Instead, it’s intended as a **principle-driven bridge** between theory and practice.

---

## 📚 Future Directions

This repo is designed to grow. Potential extensions include:

* Bayesian interferometric imaging
* Sparse reconstruction (L1 / compressed sensing)
* Integration with real data (CASA / MeqTrees)
* VLBI / EHT closure-based imaging tests

---

## 📎 References

1. *Imaging and Deconvolution*, Wilner (2014) — Primary foundation
2. YouTube Lecture (Theory of Interferometric Imaging):
   [https://www.youtube.com/watch?v=mRUZ9eckHZg](https://www.youtube.com/watch?v=mRUZ9eckHZg)