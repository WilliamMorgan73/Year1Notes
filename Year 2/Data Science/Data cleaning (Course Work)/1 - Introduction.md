# Data cleaning
Data cleaning is the transformation of data collected from customers to get rid of:
1. Missing values:
	- Salary of employees is collected over several months
	- But for some employees the information is not available for some months
2. Duplicate
	- The data for some employees is entered more than once
1. Outliers
	- Some employers came and left after several weeks
	- Information about their salaries will obfuscate the statistical analysis

# Data analytics
Data classification:  
- For example, student marks are in the range 0-100, but they are often classified into classes (70-100 first class, 60-69 upper second class and so on).  
Visualization: 
- The data is visualized by various plots (for example, histogram, bar plot, boxplot).  
Interpretation:  
- Verbal conclusions are made based on the data visualization.

# Data cleansing
Data cleansing is the process of detecting and correcting (or removing) corrupt or inaccurate records from a record set, table, or database and refers to identifying incomplete, incorrect, inaccurate or irrelevant parts of the data and then replacing, modifying, or deleting the dirty or coarse data.

# Data quality
High quality data criteria
1. Validity
2. Accuracy
3. Completeness
4. Consistency
5. Uniformity

## Validity
The degree to which the measures confirm to defined business rules or constraints
- Data-Type Constraints:
	- values in a particular column must be of a particular datatype, e.g., boolean, numeric, date, etc.  
- Range Constraints:
	- typically, numbers or dates should fall within a certain range.  
- Mandatory Constraints:
	- certain columns cannot be empty.  
- Unique Constraints:
	- a field, or a combination of fields, must be unique across a dataset.  
- Set-Membership constraints:
	- values of a column come from a set of discrete values, e.g. enum values. For example, a person’s gender may be male or female.  
- Foreign-key constraints:
	- as in relational databases, a foreign key column can’t have a value that does not exist in the referenced primary key.  
- Regular expression patterns:
	- text fields that have to be in a certain pattern. For example, phone numbers may be required to have the pattern (999) 999–9999.  
- Cross-field validation:
	- certain conditions that span across multiple fields must hold. For example, a patient’s date of discharge from the hospital cannot be earlier than the date of admission.

## Accuracy
The degree of conformity of a measure to a standard or a true value
- While defining all possible valid values allows invalid values to be easily spotted, it does not mean that they are accurate. A valid street address mightn’t actually exist.  
- Accuracy is very hard to achieve through data-cleansing in the general case because it requires accessing an external source of data that contains the true value. Accuracy has been achieved in some cleansing contexts, notably customer contact data, by using external databases that match up zip codes to geographical locations (city and state) and also help verify that street addresses within these zip codes actually exist.
- Another thing to note is the difference between accuracy and precision. Saying that you live on the earth is, actually true. But, not precise. Where on the earth?. Saying that you live at a particular street address is more precise.

## Completeness
The degree to which all required measures are known.  
- Incompleteness is almost impossible to fix with data cleansing methodology: one cannot infer facts that were not captured when the data in question was initially recorded.  
- questioning the original source if possible, say re-interviewing the subject. But the subject may give a different answer or maybe hard to reach again.
- In the case of systems that insist certain columns should not be empty, one may work around the problem by designating a value that indicates "unknown" or "missing", but the supplying of default values does not imply that the data has been made complete.

## Consistency
The degree to which the data is consistent, within the same data set or across multiple data sets.  
- Inconsistency occurs when two data items in the data set contradict each other. e.g., a customer is recorded in two different systems as having two different current addresses, and only one of them can be correct.  
- Fixing inconsistency is not always possible: it requires a variety of strategies - e.g., deciding which data were recorded more recently, which data source is likely to be most reliable (the latter knowledge may be specific to a given organization), or simply trying to find the truth by testing both data items (e.g., calling up the customer).

## Uniformity
The degree to which the data is specified using the same unit of measure.  
- In datasets pooled from different locales, weight may be recorded either in pounds or kilos.
- must be converted to a single measure using an arithmetic transformation.

## How to produce high quality data
Iterative process
1. Inspection
2. Cleaning
3. Verifying
4. Reporting

### Inspection
Exploring the underlying data for error detection  
- Data profiling: A summary statistics about the data, is really helpful to give a general idea about the quality of the data. 
	- For example, check whether a particular column conforms to a particular standard or pattern. Is the data column recorded as a string or number?
	- How many values are missing?. How many unique values in a column, and their distribution?. Is this data set is linked to or have a relationship with another?
- Visualizations
	- By analysing and visualizing the data using statistical methods such as mean, standard deviation, range, or quantiles, one can find values that are unexpected and thus erroneous.

# Cleaning
Remove, correct, or impute incorrect data
## Irrelevant data:
Those that are not actually needed, and don’t fit under the context of the problem we’re trying to solve.
Only if you are sure that a piece of data is unimportant, you may drop it. Otherwise, explore the correlation matrix between feature variables.  
And even though you noticed no correlation, you should ask someone who is domain expert. You never know, a feature that seems irrelevant, could be very relevant from a domain perspective such as a clinical perspective

## Duplicates
data points that are repeated in your dataset often happens when for example
- Data are combined from different sources
- The user may hit submit button twice thinking the form wasn’t actually submitted.
- A request to online booking was submitted twice correcting wrong information that was entered accidentally in the first time.  
A common symptom is when two users have the same identity number. Or, the same article was scrapped twice. And therefore, they simply should be removed.

## Type conversion
numbers →numerical data types.  
dates → date objects/Unix timestamp (number of seconds)  
Categorical values → numbers

## Standardize
not only recognize the typos but also put each value in the same standardized format.  
- For strings, make sure all values are either in lower or upper case.
- For numerical values, make sure all values have a certain measurement  unit. 
- For dates, the USA version is not the same as the European version. Recording the date as a timestamp (a number of milliseconds) is not the same as recording the date as a date object.

## Scaling/Transformation
Transform your data so that it fits within a specific scale, such as 0–100 or 0–1

## Missing values
Rarely clean and homogeneous.  
the missing values are unavoidable  
different data sources may indicate missing data in different ways.  
- Generally, two strategies:  
	- using a mask that globally indicates missing values,
	- or choosing a sentinel value that indicates a missing entry.
### Missing values
1. Drop
If the missing values in a column rarely happen and occur at random → drop observations  
(rows) 
If most of the column’s values are missing, and occur at random → drop the whole column
2. Impute
calculate the missing value based on other observations  
	1) Using statistical values like mean, median. However, none of these guarantees unbiased data, especially if there are many missing values.
	2) Using a linear regression. Based on the existing data, one can calculate the best fit line between twob variables, say, house price vs. size m². It is worth mentioning that linear regression models are sensitive to outliers.
	3) Hot-deck: Copying values from other similar records. This is only useful if you have enough available data. And, it can be applied to numerical and categorical data.
3. Flag
Reinforcing the pattern already exist by other features
## Outliers
Anything that lies more than $1.5 \times IQR$ away from Q1 and Q3 quartiles

## In-record $ cross-datasets errors
Two or more values in the same row or across datasets that contradict with each other

# Verifying
After cleaning the data, verify correctness by re-inspecting the data and making sure it rules and constraints do hold.  
- For example, after filling out the missing data, they might violate any of the rules and constraints.  
It might involve some manual correction if not possible otherwise.

# Reporting
Reporting how healthy the data is  
software packages or libraries can generate reports of the changes made, which rules were violated, and how many times  
In addition to logging the violations, the causes of these errors should be considered. Why did they happen in the first place?