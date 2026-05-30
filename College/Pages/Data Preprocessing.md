#college 

# Preprocessing and Data Quality

Data preprocessing is a series of steps taken to incerease the quality of  the collected data and hence, improve the efficiency and ease of the data mining process.

Data have **quality** if they satisfy the requirements of their intended use. There are many factors comprising data quality, including accuracy, completeness, consistency, timeliness, validity, and uniqueness.

Data is said to be **incomplete** if it is lacking attribute values or certain attributes of interest, or contains only aggregate data. It is said to be **inaccurate or noisy** if it contains errors, or values that deviate from the expected and **inconsistent** if it contains discrepancies.

**Timeliness** also affects data quality. For example, a month-end report is incomplete if all the data is not provided by the end of the month. Once all the data is recieved only then it becomes correct.

Two other factors affecting data quality are **believability** and **interpretability**. Believability reflects how much the data are trusted by users, while interpretability reflects how easy the data are understood. 

![[Pasted image 20260324225717.png|491]]
![[Pasted image 20260324225736.png|491]]


# Data Cleaning
Real-world data tend to be incomplete, noisy, and inconsistent. Data cleaning routines attempt to fill in missing values, smooth out noise while identifying outliers, and correct inconsistencies in the data.
## Missing Values

1. **Ignore the tuple:** This is usually done when the class label is missing (assuming the mining task involves classification). This method is not very effective, unless the tuple contains several attributes with missing values. It is especially poor when the percentage of missing values per attribute varies considerably. By ignoring the tuple, we do not make use of the remaining attributes’ values in the tuple. Such data could have been useful to the task at hand.
2. **Fill in the missing value manually:** In general, this approach is time consuming and may not be feasible given a large data set with many missing values.
3. **Use a global constant to fill in the missing value:** Replace all missing attribute values by the same constant such as a label like “Unknown” or −∞. If missing values are replaced by, say, “Unknown,” then the mining program may mistakenly think that they form an interesting concept, since they all have a value in common—that of “Unknown.” Hence, although this method is simple, it is not foolproof.
4. **Use a measure of central tendency for the attribute** (e.g., the mean or median) to fill in the missing value. For normal (symmetric) data distributions, the mean can be used, while skewed data distribution should employ the median.
5. **Use the attribute mean or median for all samples belonging to the same class as the given tuple:** If the data distribution for a given class is skewed, the median value is a better choice.
6. **Use the most probable value to fill in the missing value:** This may be determined with regression, inference-based tools using a Bayesian formalism, or decision tree induction to predict the missing values.

==Methods 3 through 6 bias the data—the filled-in value may not be correct. Method 6, however, is a popular strategy. In comparison to the other methods, it uses the most information from the present data to predict missing values.==

==Note that all missing data might not indicate incomplete data. To account for such cases, there must be one or more rules defined to account for this missing data attributes==

## Noisy Data
Noise is a random error or variance in a measured variable. There are measured through outliers in the data. Noise is introduced through human errors, errors in data collection due to faulty instruments, limited data accquisition technology etc.

### Binning 
Binning methods smooth a sorted data value by consulting its “neighborhood,” that is, the values around it. Because binning methods consult the neighborhood of values, they perform *local smoothing*. The data here must be first sorted and then partitioned into equal-frequency bins.
1. In smoothing by bin means, each value in a bin is replaced by the mean value of the bin.
2. In smoothing by bin medians, each bin value is replaced by the bin median. 
3. In smoothing by bin boundaries, the minimum and maximum values in a given bin are identified as the bin boundaries. Each bin value is then replaced by the closest boundary value.
==The larger the size of the bin(bin width), greater is the smoothening effect. Binning is also widely used as a discretization and reduction technique==
![[Pasted image 20260325110943.png|382]]

### Regression Analysis
![[Pasted image 20260325111324.png|400]]

### Outlier Analysis
Outliers may be detected by clustering, for example, where similar values are organized into groups, or “clusters.” Intuitively, values that fall outside of the set of clusters may be considered outliers.


# Data Integration
Data mining often requires data integration—the merging of data from multiple data stores. Careful integration can help reduce and avoid redundancies and inconsistencies in the resulting data set. This can help improve the accuracy and speed of the subsequent data mining process.

The semantic heterogeneity and structure of data pose great challenges in data integration. The main objective is to match schema and objects from different sources. This is the essence of the entity identification problem, ie,  are any attributes correlated? There are correlation tests for numeric(correlation coefficient and covariance test) and nominal data(chi-square test). 

Redundancy is another important issue in data integration. An attribute (such as annual revenue, for instance) may be redundant if it can be “derived” from another attribute or set of attributes.

Inconsistencies in attribute or dimension naming can also cause redundancies in the resulting data set.Tuple duplication is described detects redundancies at the tuple level. 

Data inconsistencies can be removed by Data Value Conflict Detection and Resolution
![[Pasted image 20260325113038.png|451]]

# Data Transformation

Data Transformation is a preprocessing step in which the data are transformed or consolidated so that the resulting mining process may be more efficient, and the patterns found may be easier to understand. Data discretization is a form of data transformation.

Strategies for data transformation include the following:
1. Smoothing, which works to remove noise from the data. Techniques include binning, regression, and clustering.
2. Attribute construction (or feature construction), where new attributes are constructed and added from the given set of attributes to help the mining process.
3. Aggregation, where summary or aggregation operations are applied to the data. For example, the daily sales data may be aggregated so as to compute monthly and annual total amounts. This step is typically used in constructing a data cube for data analysis at multiple abstraction levels.
4. Normalization, where the attribute data are scaled so as to fall within a smaller range, such as −1.0 to 1.0, or 0.0 to 1.0.
5. Discretization, where the raw values of a numeric attribute (e.g., age) are replaced by interval labels (e.g., 0–10, 11–20, etc.) or conceptual labels (e.g., youth, adult, senior). The labels, in turn, can be recursively organized into higher-level concepts, resulting in a concept hierarchy for the numeric attribute. More than one concept hierarchy can be defined for the same attribute to accommodate the needs of various users.
6. Concept hierarchy generation for nominal data, where attributes such as street can be generalized to higher-level concepts, like city or country. Many hierarchies for nominal attributes are implicit within the database schema and can be automatically defined at the schema definition level.

(Also see [[College/Pages/Data Discretization]])

==Data Transformation involves the Data Mapping and code generation processes==

# Data Reduction

Data reduction techniques can be applied to obtain a reduced representation of the data set that is much smaller in volume, yet closely maintains the integrity of the original data. That is, mining on the reduced data set should be more efficient yet produce the same (or almost the same) analytical results.

Data reduction strategies include dimensionality reduction, numerosity reduction, and data compression.

1.  Dimensionality reduction 
It is the process of reducing the number of random variables or attributes under consideration. Dimensionality reduction methods include wavelet transforms and principal components analysis, which transform or project the original data onto a smaller space. Attribute subset selection is a method of dimensionality reduction in which irrelevant, weakly relevant, or redundant attributes or dimensions are detected and removed.

2. Numerosity reduction techniques 
They are used to replace the original data volume by alternative, smaller forms of data representation. These techniques may be parametric or nonparametric. For parametric methods, a model is used to estimate the data, so that typically only the data parameters need to be stored, instead of the actual data. (Outliers may also be stored.) Regression and log-linear models are examples. Nonparametric methods for storing reduced representations of the data include histograms, clustering, sampling, and data cube aggregation.

3. Data compression
Here, transformations are applied so as to obtain a reduced or “compressed” representation of the original data. If the original data can be reconstructed from the compressed data without any information loss, the data reduction is called lossless. If, instead, we can reconstruct only an approximation of the original data, then the data reduction is called lossy. There are several lossless algorithms for string compression; however, they typically allow only limited data manipulation. Dimensionality reduction and numerosity reduction techniques can also be considered forms of data compression

==The computational time spent on data reduction should not outweigh or “erase” the time saved by mining on a reduced data set size.==

==Data Reduction is performed using methods such as Naive Bayes, Decision Trees, Neural network, etc==
