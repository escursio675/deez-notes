#college
(Also see Data Transformation in [[Data Discretization]])

Discretization techniques can be categorized based on how the discretization is performed, such as whether it uses class information or which direction it proceeds (i.e., top-down vs. bottom-up). If the discretization process uses class information, then we say it is supervised discretization. Otherwise, it is unsupervised. If the process starts by first finding one or a few points (called split points or cut points) to split the entire attribute range, and then repeats this recursively on the resulting intervals, it is called top down discretization or splitting. This contrasts with bottom-up discretization or merging, which starts by considering all of the continuous values as potential split-points, removes some by merging neighborhood values to form intervals, and then recursively applies this process to the resulting intervals.

Data discretization and concept hierarchy generation are also forms of data reduction. The raw data are replaced by a smaller number of interval or concept labels. This simplifies the original data and makes the mining more efficient. Concept hierarchies are also useful for mining at multiple abstraction levels.

# Discretization Methods

The following methods are applied on the assumption that-
1. Values to be discretized are sorted in ascending order
2. The methods can be applied recursively

## Binning

It is a discretization technique in which attribute values can be discretized by applying equal-width or equal-frequency binning, and then replacing each bin value by the bin mean or median, as in smoothing by bin means or smoothing by bin medians, respectively. These techniques can be applied recursively to the resulting partitions to generate concept hierarchies. Binning does not use class information and is therefore an unsupervised discretization technique. It is sensitive to the user-specified number of bins, as well as the presence of outliers.

![[Pasted image 20260325194143.png|391]]
![[Pasted image 20260325194158.png|391]]

## Entropy-Based Data Discretization
It is a supervised, top-down splitting technique that explores class distribution information in its calculation and determination of split-points.

The main idea here is to select split-points so that a given resulting partition contains as many tuples of the same class as possible. **Entropy** is the most commonly used measure for this purpose. To discretize a numeric attribute, A, the method selects the value of A that has the minimum entropy as a split-point, and recursively partitions the resulting intervals to arrive at a hierarchical discretization. Such discretization forms a **concept hierarchy** for A.

Let D consist of data instances defined by a set of attributes and a class-label attribute. The class-label attribute provides the class information per instance.

![[Pasted image 20260325195039.png|442]]
![[Pasted image 20260325195113.png|441]]
The process of determining a split-point is recursively applied to each partition obtained, until some stopping criterion is met such as-
1. When the minimum information requirement on all candidate split-points is less than a small threshold, t, or
2. When the number of intervals is greater than a threshold, max_interval

The interval boundaries (split-points) defined may help improve classification accuracy.

## Interval Merge by χ2 (Chi square) Analysis
It is a supervised bottom-up method as it uses class information. It finds the best neighboring intervals and merges them to form larger intervals recursively byt treating intervals as discrete categories. The basic notion is that for accurate discretization the relative class frequencies should be fairly consistent within an interval, therefore
if two adjacent intervals have a very similar distribution of classes then the intervals can be merged; otherwise, they should remain separate

### The Chi Merge method
1. Initially, each distinct value of a numerical attribute, A, is considered to be one interval 
2. χ2 tests are performed for every pair of adjacent intervals
3. Adjacent intervals with the least χ2 values are merged together since low χ2 values for a pair indicate similar class distributions
4. This merge process proceeds recursively until 
5. A predefined stopping criterion is met such as significance level, Max_interval, max inconsistency etc.

## Cluster Analysis

Cluster analysis is a popular data discretization method. A clustering algorithm can be applied to discretize a numeric attribute, A, by partitioning the values of A into clusters or groups. Clustering takes the distribution of A into consideration, as well as the closeness of data points, and therefore is able to produce high-quality discretization results. Clustering can be used to generate a concept hierarchy for A by following either a top-down splitting strategy or a bottom-up merging strategy, where each cluster forms a node of the concept hierarchy. In the former, each initial cluster or partition may be further decomposed into several subclusters, forming a lower level of the hierarchy. In the latter, clusters are formed by repeatedly grouping neighboring clusters in order to form higher-level concepts.

## Concept Hierarchy Generation for Categorical/Nominal Data

Concept hierarchies are a form of data discretization that can also be used for data smoothing since nominal attributes have a finite (but possibly large) number of distinct values, with no ordering among the values. It involves recursively organizing labels into higher-level concepts.
### Methods

1. **Specification of a partial ordering of attributes explicitly at the schema level by users or experts:** Concept hierarchies for nominal attributes or dimensions typically involve a group of attributes. A user or expert can easily define a concept hierarchy by specifying a partial or total ordering of the attributes at the schema level. For example, suppose that a relational database contains the following group of attributes: *street, city, province or state, and country*. A hierarchy can be defined by specifying the total ordering among these attributes at the schema level such as street < city < province or state < country.
2. **Specification of a portion of a hierarchy by explicit data grouping:** This is essentially the manual definition of a portion of a concept hierarchy. In a large database, it is unrealistic to define an entire concept hierarchy by explicit value enumeration. On the contrary, we can easily specify explicit groupings for a small portion of intermediate-level data. For example, after specifying that province and country form a hierarchy at the schema level, a user could define some intermediate levels manually, such as “{Alberta, Saskatchewan, Manitoba} ⊂ prairies_Canada” and “{British Columbia, prairies_Canada} ⊂ Western Canada.”
3. **Specification of a set of attributes, but not of their partial ordering:** A user may specify a set of attributes forming a concept hierarchy, but omit to explicitly state their partial ordering. The system can then try to automatically generate the attribute ordering so as to construct a meaningful concept hierarchy. Consider the observation that since higher-level concepts generally cover several lower-level concepts, an attribute defining a high concept level (e.g., country) will usually contain a smaller number of distinct values than an attribute defining a lower concept level (e.g., street). Based on this observation, a concept hierarchy can be automatically generated based on the number of distinct values per attribute in the given attribute set. The attribute with the most distinct values is placed at the lowest hierarchy level. The lower the number of distinct values an attribute has, the higher it is in the generated concept hierarchy. This heuristic rule works well in many cases. Some local-level swapping or adjustments may be applied by users or experts, when necessary, after examination of the generated hierarchy.
4. **Specification of only a partial set of attributes:** Sometimes a user can be careless when defining a hierarchy, or have only a vague idea about what should be included in a hierarchy. Consequently, the user may have included only a small subset of the relevant attributes in the hierarchy specification. For example, instead of including all of the hierarchically relevant attributes for location, the user may have specified only street and city. To handle such partially specified hierarchies, it is important to embed data semantics in the database schema so that attributes with tight semantic connections can be pinned together. In this way, the specification of one attribute may trigger a whole group of semantically tightly linked attributes to be “dragged in” to form a complete hierarchy. Users, however, should have the option to override this feature, as necessary.
