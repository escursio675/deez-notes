#college 

Morphology or mathematical morphology is a tool for extracting image components that are useful in the representation and description of region shape, such as boundaries, skeletons, and the convex hull.

We are interested also in morphological techniques for pre- or postprocessing, such as morphological filtering, thinning, and pruning.

These mathematical morphology are primarily implemented through set theory. In binary images, the sets in question are members of the 2-D integer space $Z^2$ whereas in grayscale images they belong to $Z^3$ and so on for coloured images etc.

Two primary, primitive operations in morphology are:

1. Reflection of a set B, denoted by $\hat{B}$:
$$
\hat{B} = \begin{cases} w|w=-b & \text{for b } \epsilon  { B\}}\end{cases}
$$
2. The translation of a set B by point z = (z1, z2), denoted (B)z, is defined as:
$$
(B)_z = \begin{cases} c|c=b+z & \text{for b } \epsilon  { B\}}\end{cases}
$$

Structuring elements (SEs) are small sets or subimages used to probe an image under study for properties of interest.

# Erosion
With A and B as sets in $Z^2$, the erosion of A by B, denoted $A \ominus B$, is defined as:
$$
A \ominus B = \{ z \mid (B)_z \subseteq A \}
$$
In words, this equation indicates that the erosion of A by B is the set of all points z such that B, translated by z, is contained in A.

## Example
![[Pasted image 20260507101544.png|558]]

We see from this example that erosion shrinks or thins objects in a binary image. In fact, we can view erosion as a morphological filtering operation in which image details smaller than the structuring element are filtered (removed) from the image. Here, erosion performed the function of a “line filter.”

# Dilation
With A and B as sets in $Z^2$, the dilation of A by B is defined as:
$$
A \oplus B = \{ z \mid (\hat{B})_z \cap A \neq \emptyset \}
$$

This equation is based on reflecting B about its origin, and shifting this reflection by z. The dilation of A by B then is the set of all displacements z, such that $\hat{B}$ and A overlap by at least one element. As before, we assume that B is a structuring element and A is the set(image objects) to be dilated.

The basic process of flipping (rotating) B about its origin and then successively displacing it so that it slides over set (image) A is analogous to spatial convolution. It must be noted, however, that dilation is based on set operations and therefore is a nonlinear operation, whereas convolution is a linear operation.

![[Pasted image 20260507115411.png|452]]

Unlike erosion, which is a shrinking or thinning operation, dilation “grows” or “thickens” objects in a binary image. The specific manner and extent of this thickening is controlled by the shape of the structuring element used. One of the simplest applications of dilation is for bridging gaps. One immediate advantage of the morphological approach over the lowpass filtering method in this context is that the morphological method resulted directly in a binary image. Lowpass filtering, on the other hand, started with a binary image and produced a grayscale image, which would require a pass with a thresholding function to convert it back to binary form.

# Opening and Closing
**Opening** generally smoothes the contour of an object, breaks narrow isthmuses, and eliminates thin protrusions. Closing also tends to smooth sections of contours but, as opposed to opening, it generally fuses narrow breaks and long thin gulfs, eliminates small holes, and fills gaps in the contour.

The opening of A by structuring element B is defined as:
$$
A \circ B = (A \ominus B) \oplus B
$$
Thus, the opening A by B is the erosion of A by B, followed by a dilation of the result by B.


And closing is defined as:
$$
A \bullet B = (A \oplus B) \ominus B
$$
which says that the closing of A by B is simply the dilation of A by B, followed by the erosion of the result by B.


Morphological operations can be used to construct filters similar in concept to the spatial filters. The objective is to eliminate the noise and its effects on an image while distorting it as little as possible. A morphological filter consisting of opening followed by closing can be used to accomplish this objective.

![[Pasted image 20260507121126.png|434]]

In general, Opening and Closing remove virtually all noise from an image by reducing light noise(erosion) and dark noise(dialation) successively from an image.

Opening is especially useful for eliminating salt noise, separating weakly connected objects, smoothing object contours, and removing thin bridges or spikes in binary images. Closing is useful for removing pepper noise, connecting fragmented regions, smoothing boundaries, and filling discontinuities in edges or contours.

# The Hit-or-Miss Transformation
The morphological hit-or-miss transform is a basic tool for shape detection. This technique uses a structuring element $B_1$ associated with objects and an element $B_2$ associated with the background based on an assumption that two or more objects are distinct only if they form disjoint sets. The morphological hit-or-miss transform of a set A by B is thus defined as:

$$
A \circledast B
=
(A \ominus B_1)
\cap
(A^c \ominus B_2)
$$
where B is the structuring element, and $B_1$ and $B_2$ are structuring foreground and background respectively.

HMT is mainly used for corner detection, junction detection, skeleton processing, shape matching etc.

# Boundary Extraction
The boundary of a set A, denoted by $\beta(A)$, can be obtained by first eroding A by B and then performing the set difference between A and its erosion. That is,
$$
\beta(A)=A-(A \ominus B)
$$
# Hole Filling
A hole may be defined as a background region surrounded by a connected
border of foreground pixels.

Let A denote a set whose elements are 8-connected boundaries, each boundary enclosing a background region (i.e., a hole). Given a point in each hole, the objective is to fill all the holes with 1s. We begin by forming an array, $X_0$, of 0s (the same size as the array containing A), except at the locations in $X_0$ corresponding to the given point in each
hole, which we set to 1. Then, the following procedure fills all the holes with 1s:

$$
X_k = (X_{k-1} \oplus B) \cap A^c
$$
where k = 1, 2, 3, ... and B is the symmetric structuring element.The algorithm terminates at iteration step k if Xk = Xk - 1. The set Xk then contains all the filled holes.The set union of Xk and A contains all the filled holes and their boundaries.

The dilation in the above equation would fill the entire area if left unchecked. However, the intersection at each step with $A^c$ limits the result to inside the region of interest.This is our first example of how a morphological process can be conditioned to meet a desired property. In the current application, it is appropriately called
_conditional dilation_.

# Extraction of Connected Components
Let A be a set containing one or more connected components, we form an array X0 (of the same size as the array containing A) whose elements are 0s (background values), except at each location known to correspond to a point in each connected component in A, which we set to 1(foreground value). The objective is to start with X0 and find all the connected components. The following iterative procedure accomplishes this objective:

$$
X_k = (X_{k-1} \oplus B) \cap A
$$
The procedure terminates when Xk = Xk - 1, with Xk containing all the connected components of the input image. The above equation is similar to _hole filling equation_ with the only difference being the use of A as opposed to its compliment as in this case, we are interested in the foreground pixel instead of background.

This technique is frequently used in automated inspections, eg, food.

# The Convex Hull
A set A is said to be convex if the straight line segment joining any two points in A lies entirely within A. The convex hull H of an arbitrary set S is the smallest convex set containing S. The set difference H - S is called the convex deficiency of S. The convex hull and convex deficiency are useful for object description. Here, we present a simple morphological algorithm for obtaining the convex hull, C(A), of a set A.

$$
X^i_k = (X_{k - 1} \circledast B^i) \cup A
$$
where i = 1, 2, 3, ... is the number of structuring elements and k = 1, 2, 3, ...

When the procedure converges (i.e., when $X^i_k$ = $X^i_{k - 1}$), we let
$D_i$ = $X^i_k$. Then the convex hull of A is

$$
C(A) = \bigcup ^ n _{i=1} D^i 
$$
where n is the number of structuring elements.

In other words, the method consists of iteratively applying the hit-or miss transform to A with $B^1$; when no further changes occur, we perform the union with A and call the result D1. The procedure is repeated with $B^2$ (applied to A) until no further changes occur, and so on. The union of the four resulting Ds constitutes the convex hull of A.

A shortcoming is that the convex hull can grow beyond the minimum dimensions required to guarantee convexity. One simple approach to reduce this effect is to limit growth so that it does not extend past the vertical and horizontal dimensions of the original set of points. However, these conditions add further computation and complexity to the algorithm.

# Thinning
The thinning of a set A by a structuring element B, denoted A z B, can be defined in terms of the hit-or-miss transform:

$$
A \otimes B
= A - (A \circledast B)
= A \cap (A \circledast B)^c
$$
Each individual thinning pass is performed until no further changes occur in A.

# Thickening
Thickening is the morphological dual of thinning and is defined by the expression:
$$
A \odot B
=
A \cup (A \circledast B)
$$
However, the usual procedure is to thin the background of the set in question and then complement the result.

Depending on the nature of A, this procedure can result in disconnected
points. Hence thickening by this method usually is followed by post-processing to remove disconnected points.

# Skeletons
Skeletons of a set are used to represent a shape using its medial axis while preserving topology.

The skeleton of a set A can be expressed in terms of erosions and openings. That is, it can be shown that:

$$
S(A)= \bigcup^K_{k=0}S_k(A)
$$
where:
$$
S_k(A)
=
(A \ominus kB)
-
\left[
(A \ominus kB)\circ B
\right]
$$
Here be is a structuring element and $(A \ominus kB)$ indicates k successive erosions of A by B. The stopping criteria is that A erodes to an empty set as:

$$
K=max\{k|(A \ominus kB)\ne \phi \}
$$
The formulation given states that S(A) can be obtained as the union of the skeleton subsets Sk(A). Also, it can be shown that A can be reconstructed from these subsets by using the equation:

$$
A=\bigcup^K_{k=0}(S_k(A) \oplus kB)
$$
Use Cases are:
- Shape representation
- Compression
- Object recognition
- Path planning

# Pruning
Pruning methods are an essential complement to thinning and skeletonizing algorithms because these procedures tend to leave parasitic components that need to be “cleaned up” by post-processing, ie, pruning removes small unwanted branches from skeletons.

To do so, we form a set X2 containing all end points in X1:

$$
X_2 = \bigcup^8_{k=1}(X_1 \circledast B^k)
$$
where 8 is the number of structuring elements.

The next step is dilation of the end points, using set A as a delimiter:
$$
X_3 = (X_2 \oplus H) \cap A
$$
where H is a 3x3 structuring element of 1s.

Finally, the union of X3 and X1 yields the desired
result:
$$
X_4 = X_1 \cup X_3
$$
Use Cases are:
- Noise removal in skeletons
- Cleaning OCR characters
- Cleaning fingerprint ridges

# Geodesic dilation and erosion
Morphological reconstruction involves two images and a structuring element. One image, the marker, contains the starting points for the transformation. The other image, the mask, constrains the transformation. The structuring element is used to define connectivity.

Let F denote the marker image and G the mask image. It is assumed in this discussion that both are binary images and that $F \subseteq G$. The geodesic dilation of size 1 of the marker image with respect to the mask, is defined as:

$$
D_G^{(1)}(F) = (F \oplus B) \cap G
$$
and the geodesic erosion of size 1 of marker F with respect to mask G
is defined as

$$
E^{(1)}(F)
=
(F \ominus B)\cup G
$$
Their iterative versions with size n are respectively:

$$
D_G^{(n)}(F)
=
D_G^{(1)}
\left[
D_G^{(n-1)}(F)
\right]
$$
with $D_G^{(0)}(F)=F$

and

$$
E_G^{(n)}(F)
=
E_G^{(1)}
\left[
E_G^{(n-1)}(F)
\right]
$$
with $E_G^{(0)}(F)=F$

Use Cases are:
1. Geodesic Dilation
	- Hole filling
	- Connected component extraction
	- Morphological reconstruction
	- Region growing
	- Marker-controlled segmentation 

2. Geodesic Erosion
	- Object extraction
	- Boundary cleanup
	- Shape simplification
	- Reconstruction filtering

## Reconstruction
The morphological reconstruction by dilation of a mask image G from a marker image F is defined as the geodesic dilation of F with respect to G, iterated until stability is achieved; that is:

$$
R_G^D(F)=D_G^{(k)}(F)
$$
with k such that $D^{(k)}_G(F)=D^{(k+1)}_G(F)$

In a similar manner, the morphological reconstruction by erosion of a mask image G from a marker image F, is defined as the geodesic
erosion of F with respect to G, iterated until stability; that is:

$$
R_G^E(F)=E_G^{(k)}(F)
$$
with k such that $E_G^{(k)}(F)=E_G^{(k+1)}(F)$.
