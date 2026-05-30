#college 
# The Discrete Wavelength Transform
### Primary Formula (Core Idea)

The DWT represents a **discrete signal** f(n) as a sum of:

- **Approximation (low-frequency) components**
- **Detail (high-frequency) components**

Forward transform:
$$
W_w(j_0, k) = \frac{1}{\sqrt{M}} \sum_{n} f(n)\, w_{j_0,k}(n)
$$
$$
W_c(j, k) = \frac{1}{\sqrt{M}} \sum_{n} f(n)\, c_{j,k}(n), \quad j \ge j_0
$$

- $W_w$​ → **approximation coefficients** (coarse/global info)
- $W_c$​ → **detail coefficients** (edges/fine details)
- k$w_{j_0,k}$, $c_{j,k}$ → **basis functions (scaled + shifted wavelets)**

---

### Inverse (Reconstruction)

$$
f(n) =
\frac{1}{\sqrt{M}} \sum_k W_w(j_0,k)\, w_{j_0,k}(n)
+
\frac{1}{\sqrt{M}} \sum_{j=j_0}^{J-1} \sum_k W_c(j,k)\, c_{j,k}(n)
$$

This ensures **perfect reconstruction** (no information loss for orthonormal bases)

---

## Core Interpretation

- DWT decomposes a signal into **multiple resolutions (scales)**:
    - Low frequency → overall structure
    - High frequency → edges, abrupt changes
- Unlike Fourier:
    - Fourier → only frequency info
    - DWT → **frequency + spatial (time) localization**

---

## Key Insight

> DWT = “analyze signal at different scales using localized wavelets”

---

## Use Cases

### 1. Image Compression

- Used in formats like **JPEG2000**
- Stores:
    - Few approximation coefficients
    - Select important detail coefficients
- Achieves **high compression with minimal quality loss**

---

### 2. Edge Detection / Feature Extraction

- Detail coefficients highlight:
    - Edges
    - Discontinuities
- Useful in:
    - Computer vision
    - Medical imaging

---

### 3. Noise Removal (Denoising)

- Noise appears in **high-frequency coefficients**
- Strategy:
    - Threshold small detail coefficients
    - Keep significant ones
- Result → clean signal/image

---

### 4. Multiresolution Analysis

- Same signal viewed at:
    - Coarse scale (global view)
    - Fine scale (details)
- Useful in:
    - Progressive image transmission
    - Pattern recognition

---

## One-Line Summary

> DWT decomposes a discrete signal into **coarse (approximation) and fine (detail) components across multiple scales**, enabling efficient analysis, compression, and reconstruction.


# DWT in 2 Dimensions
### Primary Formula (Separable 2D DWT)

The 2D DWT is obtained by applying the 1D DWT **first along rows, then along columns** (separable filtering):
$$
\begin{cases}
L_r(x,y) = \sum_n f(x,n)\,h(y-n) \\
H_r(x,y) = \sum_n f(x,n)\,g(y-n)
\end{cases}
$$

Then column transform:
$$
\begin{cases}
LL(x,y) = \sum_m L_r(m,y)\,h(x-m) \\
LH(x,y) = \sum_m L_r(m,y)\,g(x-m) \\
HL(x,y) = \sum_m H_r(m,y)\,h(x-m) \\
HH(x,y) = \sum_m H_r(m,y)\,g(x-m)
\end{cases}
$$

- h → low-pass filter (approximation)
- g → high-pass filter (detail)

## Subbands Interpretation

After one level of decomposition, the image is split into 4 subbands:

- **LL (Low-Low)**
    - Low-pass in both directions
    - Represents **coarse / approximation image**
- **LH (Low-High)**
    - Low-pass rows, high-pass columns
    - Captures **horizontal edges**
- **HL (High-Low)**
    - High-pass rows, low-pass columns
    - Captures **vertical edges**
- **HH (High-High)**
    - High-pass in both directions
    - Captures **diagonal details / fine textures**
## Multilevel Decomposition

The LL subband is recursively decomposed:
$$
\text{Level } j: \quad LL_{j-1} \rightarrow \{LL_j, LH_j, HL_j, HH_j\}
$$
Each level gives:

- Lower resolution approximation
- New detail components at that scale

## Core Idea

> 2D DWT decomposes an image into **frequency subbands across both directions**, enabling analysis of edges and textures at multiple scales.

---

## Use Cases

### 1. Image Compression (Most Important)

- Most energy concentrated in **LL subband**
- Many coefficients in LH, HL, HH are small → discardable
- Basis of **JPEG2000**

---

### 2. Edge Detection

- LH → horizontal edges
- HL → vertical edges
- HH → diagonal features
- Useful for feature extraction

---

### 3. Image Denoising

- Noise mostly in **high-frequency bands (LH, HL, HH)**
$$
|C| < T \Rightarrow C = 0
$$
- Thresholding removes noise while preserving structure

---

### 4. Multiresolution Analysis

- Coarse-to-fine representation
- Useful in:
    - Progressive transmission
    - Object detection
    - Pattern recognition

---

## One-Line Summary

> 2D DWT decomposes an image into **LL, LH, HL, HH subbands and recursively refines LL**, enabling efficient multiscale analysis, compression, and feature extraction.


