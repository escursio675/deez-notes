#college 

A **data object** represents an entity that is described by a set of *attributes*. Data objects can also be referred to as samples, examples, instances, data points, or objects. If the data objects are stored in a database, they are called data tuples.

==Note: **Data** refers to to distinct pieces of information, usually formatted and stored in a way that is efficient for movement or processing==

# Attributes
An attribute is a data field, representing a characteristic or feature of a data object. The nouns attribute, dimension, feature, and variable are often used interchangeably. 

Observed values for a given attribute are known as observations.

A set of attributes used to describe a given object is called an attribute vector (or feature vector). The distribution of data involving one attribute (or variable) is called univariate. A bivariate distribution involves two attributes, and so on.

The type of an attribute is determined by the set of possible values—nominal, binary, ordinal, or numeric—the attribute can have.
## Types of Attributes

==Note: There are many ways of organising attributes. These types of attributes are not mutually exclusive==
### Qualitative Attributes
Qualitative attributes describe a feature of an object without giving an actual size or quantity. The values of such qualitative attributes are typically words representing categories.

#### Nominal Attributes 
They are symbols or names of things. Each value represents some kind of category, code, or state, and so nominal attributes are also referred to as categorical. The values do not have any meaningful order. In computer science, the values are also known as enumerations. Such names or categories can be mapped to numbers; however, this do not make them numerical attributes as they are not meant to be used quantitatively, ie, any mathematical operations on them do not carry any meaning.

==One such operation that IS of interest is the most commonly occurring value, ie, the *mode*==

#### Binary Attributes
They are nominal attributes with only two categories or states: 0 or 1, where 0 typically means that the attribute is absent, and 1 means that it is present. Binary attributes are referred to as Boolean if the two states correspond to true and false. 

A binary attribute is symmetric if both of its states are equally valuable and carry the same weight; that is, there is no preference on which outcome should be coded as 0 or 1. One such example could be the attribute gender having the states male and female. A binary attribute is asymmetric if the outcomes of the states are not equally important, such as the positive and negative outcomes of a medical test for HIV. By convention, we code the most important outcome, which is usually the rarest one, by 1 (e.g., HIV positive) and the other by 0 (e.g., HIV negative).

#### Ordinal Attributes 
They are attributes with possible values that have a meaningful order or ranking among them, but the magnitude between successive values is not known.

For example, The nominal attribute *size_of_drink* has three possible values: small, medium, and large but we do not know how larger a medium drink is than a small and so on.

Ordinal attributes are useful for registering subjective assessments of qualities that cannot be measured objectively. They may also be obtained from the discretization of numeric quantities by splitting the value range into a finite number of ordered categories. The central tendency of an ordinal attribute can be represented by its mode and its median (the middle value in an ordered sequence), but the mean cannot be defined.


### Quantitative Attributes

#### Numeric Attributes
They are used to represent a measurable quantity, as integer or real values. Numeric attributes can be interval-scaled or ratio-scaled.

##### Interval-Scaled Attributes
Interval-scaled attributes are measured on a scale of equal-size units. The values of
interval-scaled attributes have order and can be positive, 0, or negative. Thus, in addition to providing a ranking of values, such attributes allow us to compare and quantify the difference between values.

For example, temperature since a temperature of 20◦ C is five degrees higher than a temperature of 15◦ C. Calendar dates are another example.

##### Ratio-Scaled Attributes
Temperatures in Celsius and Fahrenheit do not have a true zero-point, that is, neither 0◦ C nor 0◦ F indicates “no temperature.” Similarly, the calendar date 0 does not exist. This prevents us from expressing these values in terms of ratios, therefore we have ratio-scaled values that have a "true zero".

A ratio-scaled attribute is a numeric attribute with an inherent zero-point. That is, if
a measurement is ratio-scaled, we can speak of a value as being a multiple (or ratio)
of another value. In addition, the values are ordered, and we can also compute the
difference between values, as well as the mean, median, and mode. Example, temperature in Kelvin, *years_of_experience* , *number_of_words* etc

#### Discrete and Continuous Attributes
A discrete attribute has a finite or countably infinite set of values, which may or may not be represented as integers. If an attribute is not discrete, it is continuous.

In practice, real values are represented using a finite number of digits. Continuous attributes are typically represented as floating-point variables. Example, survey scores like 0.5, 1.0, 1.5, 2.0 are discrete since they have only some specific values(not every real number possible) whereas height, sensor readings etc are continuous values.

