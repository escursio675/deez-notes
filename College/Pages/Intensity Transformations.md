#college 


**Spatial Domain** is the plane containing the pixels of an image. Spatial domain techniques operate directly on the pixels of an image. Generally, spatial domain techniques are more efficient computationally and require less processing resources to implement(as opposed to frequency domain techniques).

### Spatial Filtering

The operations applied can be expressed as g(x, y) = T[ f(x, y)]

Here f represents the neighborhood of points with origin at x, y which, in turn is a small part of the image. The transform T is applied over the the entire image, one such pixel neighborhood at a time. This process continues from the top-left pixel to the bottom-right in the form of horizontal scans and any missing pixels at the boundary origins are either ignored, or padded with values 0. This entire process is called **spatial filtering**.

The neighborhood, along with a predefined operation, is called a spatial filter (also referred to as a spatial mask, kernel, template, or window).

### Intensity Transformation

The smallest possible neighborhood is of size 1 * 1. In this case, g depends only on the value of f at a single point (x, y) and T becomes an intensity (also called gray-level or mapping) transformation function of the form
$$
s = T(r)
$$
where, for simplicity in notation, s and r are variables denoting, respectively, the intensity of g and f at any point (x, y).

### Image Enhancement

Enhancement is the process of manipulating an image so that the result is more suitable than the original for a _**specific**_ application. Specific, meaning that that the enhancement techniques are most often, problem oriented. Thus, for example, a method that is quite useful for enhancing X-ray images may not be the best approach for enhancing satellite images taken in the infrared band of the electromagnetic spectrum.

# Intensity Transform Functions

Intensity transformations are among the simplest of all image processing techniques. Because we are dealing with digital quantities, values of a transformation function typically are stored in a one-dimensional array and the mappings from r to s are implemented via table lookups. For an 8-bit environment, a lookup table containing the values of T will have 256 entries.

![[image(5).png|321]]

## Image Negatives

The negative of an image with intensity levels in the range [0, L - 1] is obtained by using the negative transformation which is given by the expression $s = L - 1 - r$

Reversing the intensity levels of an image in this manner produces the equivalent of a photographic negative. This type of processing is particularly suited for enhancing white or gray detail embedded in dark regions of an image, especially when the black areas are dominant in size.

## Log Transforms

The general form of the log transformation is $s = c log (1 + r)$

where c is a constant, and it is assumed that r ≥ 0. The shape of the log curve in shows that this transformation maps a narrow range of low intensity values in the input into a wider range of output levels. The opposite is true of higher values of input levels. We use a transformation of this type to expand the values of dark pixels in an image while compressing the higher-level values. The opposite is true of the inverse log transformation. Any curve having the general shape of the log functions shown in would accomplish this spreading/compressing of intensity levels in an image, but the power-law transformations discussed in the next section are much more versatile for this purpose. The log function has the important characteristic that it compresses the dynamic range of images with large variations in pixel values.

It is not unusual to encounter spectrum values that range from 0 to 10^6 or higher. While processing numbers such as these presents no problems for a computer, image display systems generally will not be able to reproduce faithfully such a wide range of intensity values. The net effect is that a significant degree of intensity detail can be lost in the display. When these values are scaled linearly for display in an 8-bit system, the brightest pixels will dominate the display, at the expense of lower (and just as important) values of the spectrum. If, instead of displaying the values in this manner, we first apply log transform(with c = 1 in this case) to the spectrum values, then the range of values of the result becomes 0 to 6.2, which is more manageable.

Most of the Fourier spectra seen in image processing publications have been scaled in just this manner.

## Power Law/Gamma Transforms

Power-law transformations have the basic form $s = c r^\gamma$

where c and g are positive constants. Sometimes the equation is written as $s = c(r + \epsilon)^\gamma$ to account for an offset (that is, a measurable output when the input is zero). However, offsets typically are an issue of display calibration and as a result they are normally ignored. The gamma function is similar to the log function however, we can obtain a family of possible transformation curves simply by varying g.

![[image(6).png|356]]

The curves at gamma > 1 have exactly the opposite effect as that of gamma < 1 with c = g = 1 reducing the equation to identity.

A variety of devices used for image capture, printing, and display respond according to a power law. The process used to correct these power-law response phenomena is called **gamma correction**. For example, cathode ray tube (CRT) devices have an intensity-to-voltage response that is a power function, with exponents varying from approximately 1.8 to 2.5. With reference to the curve for g = 2.5 we see that such display systems would tend to produce images that are darker than intended. Gamma correction in this case is straightforward. All we need to do is preprocess the input image before inputting it into the monitor by performing the transformation s = $r^{\frac{1}{2.5}}$ = $r^{0.4}$. produces an output that is close in appearance to the original image.

A similar analysis would apply to other imaging devices such as scanners and printers. The only difference would be the device-dependent value of gamma.

Note: Gamma correct also changes the ratios of RGBs in an image

For example, to account for the gamma correction of various display devices used, websites preprocess stored images with an “average” of the gamma values of all display devices currently in the market.

Note: To make darker parts of an image more visible we would use fractional values of gamma. However, reducing the value of this fraction past a certain point makes the image appear “washed-out” and compromises on the contrast and increasing it to provide lighter images more contrast can hide details in the darker regions of the image.

# Piecewise-Linear Transformation Functions

A complementary approach to the methods discussed for intensity transformations is to use piecewise linear functions. The principal advantage of piecewise linear functions is that we can introduce additional complexity “arbitrarily” into such transforms, much more than the previous transformations.

## Contrast Stretching

Low-contrast images can result from poor illumination, lack of dynamic range in the imaging sensor, or even the wrong setting of a lens aperture during image acquisition

**Contrast stretching** is a process that expands the range of intensity levels in an image so that it spans the full intensity range of the recording medium or display device.

The locations of points (r1, s1) and (r2, s2) control the shape of the transformation function. If r1 = s1 and r2 = s2, the transformation is a linear function that produces no changes in intensity levels as shown below.

![[image(9).png|243]]

If r1 = r2, s1 = 0 and s2 = L - 1, the transformation becomes a **thresholding function** that creates a binary image, as illustrated

![[image(7).png|217]]

Intermediate values of (r1, s1) and (r2, s2) produce various degrees of spread in the intensity levels of the output image, thus affecting its contrast. In general, r1 … r2 and s1 … s2 is assumed so that the function is single valued and monotonically increasing(relative brightness of pixels stays the same after processing). This condition preserves the order of intensity levels, thus preventing the creation of intensity artifacts in the processed image.

Note: **Intensity artifacts** are **unnatural visual effects** introduced during image processing, such as: strange brightness patches false edges bending or distortion in smooth areas.

Note: To stretch the image intensity to the full range of [0, L -1] we can set (r1, s1) = ($r_{min}$, 0) and (r2, s2) = ($r_{max}$, L - 1), where $r_{min}$ and $r_{max}$ denote the minimum and maximum intensity levels in the image, respectively

## Intensity-level Slicing

Highlighting a specific range of intensities in an image often is of interest.Applications include enhancing features such as masses of water in satellite imagery and enhancing flaws in X-ray images. The process, often called **intensity-level slicing**, can be implemented in several ways, but most are variations of two basic themes. One approach is to display in one value (say, white) all the values in the range of interest and in another (say, black) all other intensities. This transformation, shown below(left), produces a binary image. This type of transformation is used when the interest lies in the _shape._

The second approach, based on the transformation below(right), brightens (or darkens) the desired range of intensities but leaves all other intensity levels in the image unchanged. This is used when we are interested in measuring the flow of contrast medium as a function of time through a series of images.

![[image(8).png|433]]


# Histogram Processing
The histogram of a digital image with intensity levels in the range [0,L - 1] is a discrete function $h(r_k) = n_k$, where $r_k$ is the kth intensity value and $n_k$ is the number of pixels in the image with intensity $r_k$. It is common practice to normalize a histogram by dividing each of its components by the total number of pixels in the image, denoted by the product MN, where, as usual, M and N are the row and column dimensions of the image. Thus, a normalized histogram is given by $p(r_k) = r_k >MN$, for k = 0, 1, 2, ..., L - 1. Loosely speaking, $p(r_k)$ is an estimate of the probability of occurrence of intensity level $r_k$ in an image. The sum of all components of a normalized histogram is equal to 1.

Histograms, being simple to calculate in software, serve as a basis for multiple spatial domain processing like image enhancement, compression and visualization of image statistics.

Histograms in which the components are uniformly distributed in the entire range imply images with high contrast and high dynamic range, as opposed to washed-out, dull images. It is possible to increase the range of the histogram through histogram equilization and hence improve the contrast of the image.

## Histogram Equilization

The discrete form of the **histogram equalization** or **histogram linearization transformation** is:

$$
s_k = T(r_k) = (L - 1) \sum_{j=0}^k p_r(r_j) = \frac{L-1}{MN}\sum_{j=0}^k n_j
$$
where k = 0, 1, 2, ..., L - 1

In the above function, hence, a processed (output) image is obtained by mapping each pixel in the input image with intensity $r_k$ into a corresponding pixel with level $s_k$.

This function has the general tendency to spread the components of an image through the entire range of intensities leading to image enhancement. Note that this is an "adaptive" image enhancement transformation, meaning histogram equalization renders any intensity differences in the equalized images with same content visually indistinguishable.

It is assumed that, for the above function, the following hold for considerations of (a) output values cannot be less than their corresponding input values (b) range of output and input intensities should be same (a') mappings from s back to r must be one-one to prevent ambiguities.

(a) T(r) is a monotonically increasing function in the interval 
0 <= r <= L - 1
(b) 0 <= T(r) <= L - 1 for 0 <= r <= L - 1.
(c) T(r) is a strictly monotonically increasing function in the interval
0 <= r <= L - 1

where the inverse function corresponding to (c) is 
$$
r_k = T^{-1}(s_k)
$$
where k = 0, 1, 2, ... , L - 1

This inverse transformation satisfies conditions (a') and (b) only if none of the levels, rk, k = 0, 1, 2, ... , L - 1, are missing from the input image, which in turn means that none of the components of the image histogram are zero.

==In case of fractional values, they are rounded to the nearest integer==


# Spatial Filtering
“Filtering” refers to accepting (passing) or rejecting certain frequency components. For example, a filter that passes low frequencies is called a lowpass filter. The net effect produced by a lowpass filter is to blur (smooth) an image. We can accomplish a similar smoothing directly on the image itself by using spatial filters (also called spatial masks, kernels, templates, and windows).

Spatial filters consists of 
1. a neighborhood, (typically a small rectangle)
2. a predefined operation that is performed on the image pixels encompassed by the neighborhood. 

Filtering creates a new pixel with coordinates equal to the coordinates of the center of the neighborhood, and whose value is the result of the filtering operation. A processed (filtered) image is generated as the center of the filter visits each pixel in the input image. If the operation performed on the image pixels is linear, then the filter is called a **linear spatial filter**. Otherwise, the filter is
**nonlinear**.

## Correlation and Convolution

**Correlation** is the process of moving a filter mask over the image
and computing the sum of products at each location. The mechanics of **convolution** are the same, except that the filter is first rotated by 180°.

If $f$ is a function to which we apply a mask of size m x n, then $f$ must be padded with at least m - 1 rows of zeroes on the top and bottom and n - 1 columns of zeroes on either side of the image. After correlation, the padded resulting function is often again cropped to the original size of $f$.

A function that contains a single 1 with the rest being 0s is called  a **discrete unit impulse**, which esentially copies the window but rotated by 180deg at the location of the impulse.

Therefore, if we pre-rotate either $f$ or the window by 180deg, the desired result, ie, the copy of the function at the location of the impulse is obtained. This process is called **convolution**.

==If the filter mask is symmetric, correlation and convolution yield the same result.==


If, instead of containing a single 1s, image f had contained a region identically equal to w, the value of the correlation function (after normalization) would have been maximum when w was centered on that region of f. Thus, correlation can be used also to find matches between images.

![[Pasted image 20260506090447.png|417]]

Thus, correlation of a filter w(x, y) of size m * n with an image f(x, y), denoted as w(x, y) * f(x, y), is given by the equation:
$$w(x, y) * f(x, y) = \sum_{s=-a}^a\sum_{t=-b}^b w(s, t)f(x + s, y + t)$$
where a = (m - 1)/2, b = (n - 1)/2 and x, y as displacement variables such that w vists every pixel in f

Similarly, convolution is given by
$$w(x, y) * f(x, y) = \sum_{s=-a}^a\sum_{t=-b}^b w(s, t)f(x - s, y - t)$$

## Smoothing Spatial Filters
Smoothing filters are used for blurring and for noise reduction. Blurring is used in preprocessing tasks, such as removal of small details from an image prior to (large) object extraction, and bridging of small gaps in lines or curves. Noise reduction can be accomplished by blurring with a linear and  nonlinear filtering.

The output of a smoothing, linear spatial filter is simply the average of the pixels contained in the neighborhood of the filter mask. These filters sometimes are called averaging filters or lowpass filters.

Because random noise typically consists of sharp transitions in intensity levels, the most obvious application of smoothing is noise reduction. However, edges (which almost always are desirable features of an image) also are characterized by sharp intensity transitions, so averaging filters have the undesirable side effect that they blur edges.

Smoothing filters are also used to reduces irrelevant details in the image, ie, details that are smaller than the size of the filter mask. Therefore, the size of the mask is chosen as per the size of the details to be "blurred out". The expression is as follows:

$$
g(x, y) = \frac{\sum_{s=-a}^a\sum_{t=-b}^b w(s, t)f(x + s, y + t)}{\sum_{s=-a}^a\sum_{t=-b}^b w(s, t)}
$$
The denominator is simply the sum of the mask coefficients and, therefore, it is a constant that needs to be computed only once. In general, for an m x n mask, the value is expressed by:

$$
R = \frac{1}{mn}\sum_{i=i}^{mn}r_i
$$

	Order-statistics or nonlinear filters perform smoothning based on the ranking of intensity values. A well known filter is the median filter which is particularly useful for _salt and pepper noise_ or impulse noise. A median mask essentially forces the value of a pixel to be like its neighbours. The median filter thus, represents the 50th percentile of ranked pixel intensities. The so called _max filter_ targets the 100th percentile, used for finding the brightest points in an image, similarly for the _min filter.

## Sharpening Spatial Filters
The principal objective of sharpening is to highlight transitions in intensity. Uses of image sharpening vary and include applications ranging from electronic printing and medical imaging to industrial inspection and autonomous guidance in military systems. Because blurring is accomplished by averaging of pixel values implemented through integration, it is logical to conclude that sharpening can be accomplished by spatial differentiation, specifically by the Laplacian $\nabla^2f(x,y)$.

Because the Laplacian is a derivative operator, its use highlights intensity discontinuities in an image and deemphasizes regions with slowly varying intensity levels. This will tend to produce images that have grayish edge lines and other discontinuities, all superimposed on a dark, featureless background. Background features can be “recovered” while still preserving the sharpening effect of the Laplacian simply by adding the Laplacian image to the original, keeping in mind the sign of the result of the Laplacian. It must be kept in mind that the Laplacian increases the contrast at the locations of intensity discontinuities.

A similar effect can be obtained using the first-order derivatives through gradients. The gradient can be used also to highlight small specs that may not be readily visible in a gray-scale image. The ability to enhance small discontinuities in an otherwise flat gray field is another important feature of the gradient. Gradients are discussed in further details in [[Image Segmentation]].