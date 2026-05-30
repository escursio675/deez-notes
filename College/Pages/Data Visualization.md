#college 

Data visualization aims to communicate data clearly and effectively through graphical representation. Data visualization has been
used extensively in many applications—for example, at work for reporting, managing business operations, and tracking progress of tasks. More popularly, we can take advantage of visualization techniques to discover data relationships that are otherwise not easily observable by looking at the raw data.

# Pixel-Oriented Visualization Techniques
A simple way to visualize the value of a dimension is to use a pixel where the color of
the pixel reflects the dimension’s value. For a data set of m dimensions, pixel-oriented
techniques create m windows on the screen, one for each dimension. The m dimension
values of a record are mapped to m pixels at the corresponding positions in the windows.
The colors of the pixels reflect the corresponding values.
Inside a window, the data values are arranged in some global order shared by all
windows. The global order may be obtained by sorting all data records in a way that’s
meaningful for the task at hand.

# Geometric Projection Visualization Techniques

A drawback of pixel-oriented visualization techniques is that they cannot help us much
in understanding the distribution of data in a multidimensional space. For example, they
do not show whether there is a dense area in a multidimensional subspace. Geometric projection techniques help users find interesting projections of multidimensional data
sets. The central challenge the geometric projection techniques try to address is how to
visualize a high-dimensional space on a 2-D display. Examples are scatter plots, scatter-plot matrices, parallel coordinates.

# Icon-Based Visualization Techniques

Icon-based visualization techniques use small icons to represent multidimensional
data values. Two popular icon-based techniques are Chernoff faces and stick
figures.