#college 

|   |   |
|---|---|
|Restoration techniques|**5.3–5.10**|

|   |   |
|---|---|
|Noise restoration filters|**5.3 Restoration in the Presence of Noise Only—Spatial Filtering**|

|   |   |
|---|---|
|Adaptive filters|**5.3.3 Adaptive Filters**|

|   |   |
|---|---|
|Linear, Position-Invariant degradations|**5.5 Linear, Position-Invariant Degradations**|

|   |   |
|---|---|
|Estimation of degradation functions|**5.6 Estimating the Degradation Function**|

|                              |                                                |
| ---------------------------- | ---------------------------------------------- |
| Restoration from projections | **5.11 Image Reconstruction from Projections** |


Restoration attempts to recover an image that has been degraded by using a prior knowledge of the degradation phenomenon. Thus, restoration techniques are oriented toward modeling the degradation and applying the inverse process in order to recover the original image.

# The Degradation/Restoration Model
A degradation function that, together with an additive noise term, operates on an input image f(x, y) to produce a degraded image g(x, y). Given g(x, y), some knowledge about the degradation function H, and some knowledge about the additive noise term $\eta(x, y)$, the objective of restoration is to obtain an estimate $\hat{f}(x, y)$ of the original image.

==Here we will assume degradations due to noise only==

If H is a linear, position-invariant process, then the degraded image is given in the spatial domain by:
$$
g(x, y) = h(x, y) *f(x, y) + \eta(x, y)
$$
where h(x, y) is the spatial representation of the degradation function and * is convolution.

Since convolution in the spatial domain is analogous to multiplication in the frequency domain, we may derive the following equivalent frequency domain representation:
$$
G(u, v) = H(u, v)F(u, v) + N(u, v)
$$
where the terms in capital letters are the Fourier transforms of the corresponding terms.

# Noise Models
The principal sources of noise in digital images arise during image acquisition and/or transmission.

## Spatial and Frequency Properties of Noise
Relevant to our discussion are parameters that define the spatial characteristics of noise, and whether the noise is correlated with the image. Frequency properties refer to the frequency content of noise in the Fourier sense. For example, when the Fourier spectrum of noise is constant, the noise usually is called white noise.

### Some Important Noise Probability Density Functions
The spatial noise descriptor with which we shall be concerned is the statistical behaviour of the intensity values in the noise component. These may be considered random variables, characterized by a probability density function(PDF).

1. Gaussian/Normal Noise
The PDF of a Gaussian random variable, z, is given by:
$$
p(z)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(z-\mu)^2}{2\sigma^2}}
$$
2. Rayleigh Noise
$$
p(z)=
\begin{cases}
\frac{2}{b}(z-a)e^{-\frac{(z-a)^2}{b}}, & z \ge a \\
0, & z<a
\end{cases}
$$
where:
- a = location parameter
- b = scale parameter

3. Erlang (Gamma) Noise
$$p(z)=
\begin{cases}
\frac{a^b z^{b-1}}{(b-1)!}e^{-az}, & z\ge0 \\
0, & z<0
\end{cases}$$
where:
- a>0
- b = positive integer
4. Exponential Noise
$$
p(z)=
\begin{cases}
ae^{-az}, & z\ge0 \\
0, & z<0
\end{cases}
$$
where a > 0

5. Uniform Noise
$$
p(z)=
\begin{cases}
\frac{1}{b-a}, & a\le z \le b \\
0, & \text{otherwise}
\end{cases}
$$
where:
- a = lower bound
- b = upper bound
6. Impulse(Salt and Pepper) Noise
$$
p(z)=
\begin{cases}
P_a, & z=a \\
P_b, & z=b \\
0, & \text{otherwise}
\end{cases}
$$
where:
- a = pepper intensity (dark)
- b = salt intensity (bright)
- $P_a, P_b$ = probabilities of occurrence

7. Periodic Noise
This type of noise is spatially dependent and can be reduced significantly via frequency domain filtering.

### Estimation of Noise Parameters
The parameters of periodic noise typically are estimated by inspection of the Fourier spectrum of the image. Periodic noise tends to produce frequency spikes that often can be detected even by visual analysis. Another approach is to attempt to infer the periodicity of noise components directly from the image, but this is possible only in simplistic cases. Partial parameters may be available through the image acquisition sensors or may not be. In both cases, some estimation of the parameters are required.

The simplest use of the data from the image is calculating the mean
and variance of intensity levels. The shape of the histogram identifies the closest PDF match. If the shape is approximately Gaussian, then the mean and variance are sufficient. to solve for the parameters a and b. Impulse noise is handled differently because the estimate needed is of the actual probability of occurrence of white and black pixels.

# Restoration in the presence of Noise only
When the only degradation present in an image is noise, we have:
$$
g(x, y) = *f(x, y) + \eta(x, y)
$$
and:
$$
G(u, v) = F(u, v) + N(u, v)
$$
The filtering of this additive noise is as follows:

## Mean filters

### Arithmetic mean filter
The arithmetic mean filter computes the average value of the corrupted
image g(x, y) in the area defined by subimage Sxy. The filter smooths local variations in an image, and noise is reduced as a result of blurring. AMF is best suited for Gaussian and uniform noise.
$$
\hat{f}(x,y)=\frac{1}{mn}\sum_{(s,t)\in S_{xy}} g(s,t)
$$
### Geometric mean filter
Here, each restored pixel is given by the product of the pixels in the subimage window, raised to the power 1/mn. The smoothing comparable to the arithmetic mean filter, but it tends to lose less image detail in the process.
$$
\hat{f}(x,y)=\left[\prod_{(s,t)\in S_{xy}} g(s,t)\right]^{\frac{1}{mn}}
$$
### Harmonic mean filter
The harmonic mean filter works well for salt noise, but fails for pepper noise. It does well also with other types of noise like Gaussian noise.
$$
\hat{f}(x,y)=
\frac{mn}
{\displaystyle \sum_{(s,t)\in S_{xy}} \frac{1}{g(s,t)}}
$$
### Contraharmonic mean filter
where Q is called the order of the filter. This filter is well suited for reducing or virtually eliminating the effects of salt-and-pepper noise. For positive values of Q, the filter eliminates pepper noise. For negative values of Q it eliminates salt noise. It cannot do both simultaneously. Note that the contraharmonic filter reduces to the arithmetic mean filter if Q = 0, and to the harmonic mean filter if Q = -1.
$$
\hat{f}(x,y)=
\frac
{\displaystyle \sum_{(s,t)\in S_{xy}} g(s,t)^{Q+1}}
{\displaystyle \sum_{(s,t)\in S_{xy}} g(s,t)^Q}
$$
The contraharmonic filter is well suited for impulse noise assuming it is known if the noise is dark or white.

## Order-statistics filters
Order-statistic filters are spatial filters whose response is based on ordering (ranking) the values of the pixels contained in the image area encompassed by the filter.

### Median
Median filters are quite popular because, for certain types of random noise, they provide excellent noise-reduction capabilities, with considerably less blurring than linear smoothing filters of similar size. Median filters are particularly effective in the presence of both bipolar and unipolar impulse noise.
$$
\hat{f}(x,y)=\operatorname{median}_{(s,t)\in S_{xy}} \{g(s,t)\}
$$

### Max and Min filters
This filter is useful for finding the brightest points in an image. Also, because pepper noise has very low values, it is reduced by this filter as a result of the max selection process in the subimage area Sxy. Similarly for min filters.
$$
\hat{f}(x,y)=\max_{(s,t)\in S_{xy}} \{g(s,t)\}
$$

$$
\hat{f}(x,y)=\min_{(s,t)\in S_{xy}} \{g(s,t)\}
$$
### Midpoint
It works best for randomly distributed noise, like Gaussian or uniform noise.
$$
\hat{f}(x,y)=
\frac{1}{2}
\left[
\max_{(s,t)\in S_{xy}}\{g(s,t)\}
+
\min_{(s,t)\in S_{xy}}\{g(s,t)\}
\right]
$$

### Alpha-Trimmed Mean filter
When d = 0, the alpha- trimmed filter reduces to the arithmetic mean filter discussed in the previous section. If we choose d = mn - 1, the filter becomes a median filter. For other values of d, the alpha-trimmed filter is useful in situations involving multiple types of noise, such as a combination of salt-and-pepper and Gaussian noise.
$$
\hat{f}(x,y)=
\frac{1}{mn-d}
\sum_{(s,t)\in S_{xy}} g_r(s,t)
$$
## Adaptive Filters
Adaptive filter behaviour changes based on statistical characteristics of the image inside the filter region defined by the m * n rectangular window Sxy. As the following discussion shows, adaptive filters are capable of performance superior to that of the filters discussed thus far. The price paid for improved filtering power is an increase in filter complexity.

Used when:
- noise variance changes across the image
- some regions are smooth while others contain edges/details
- you want to reduce noise without heavily blurring edges

They are used mainly for Gaussian, additive random and spatially varying noises.

### Adaptive, local noise reduction filter
Over a local region, Sxy, the response of the filter at any point (x, y) on which the region is centered is to be based on four quantities:
(a) g(x, y), the value of the noisy image at (x, y)
(b) $\sigma^2_{\eta}$, the variance of the noise corrupting f(x, y) to form g(x, y)
(c) $m_L$, the local mean of the pixels in Sxy
(d) $\sigma^2_L$, the local variance of the pixels in Sxy.

We want the behavior of the filter to be as follows:
1. If $\sigma^2_{\eta}$ is zero, the filter should return simply the value of g(x, y). This is the trivial, zero-noise case in which g(x, y) is equal to f(x, y).
2. If the local variance is high relative to $\sigma^2_{\eta}$, the filter should return a value close to g(x, y). A high local variance typically is associated with edges, and these should be preserved.
3. If the two variances are equal, we want the filter to return the arithmetic mean value of the pixels in Sxy. This condition occurs when the local area has the same properties as the overall image, and local noise is to be reduced simply by averaging.

The only quantity that needs to be known or estimated is the variance of the overall noise, s2h. The other parameters are computed from the pixels in Sxy at each location (x, y) on which the filter window is centered.

### Adaptive meadian filter
