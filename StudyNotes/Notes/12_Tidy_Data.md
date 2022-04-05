# Tidy Data

## Index

**[Defining Tidy Data](#Defining Tidy Data)**
	[Data Structure](#Data Structure)
	[Data Semantics](#Data Semantics)
	[Tidy Data](#Tidy Data)

**[Tidying Messy Datasets](#Tidying Messy Datasets)**
	[Column headers are values, not variable names](#Column headers are values, not variable names)
	[Multiple Variables Stored in one column](#Multiple Variables Stored in one column)
	[Variables are stored in both rows and columns](#Variables are stored in both rows and columns)
	[Multiple types in one table](#Multiple types in one table)
	[One type in multiple tables](One type in multiple tables)

**[Tidy Tools](#Tidy Tools)**
	[Manipulation](#Manipulation)
	[Visualization](#Visualization)
	[Modeling](#Modeling)



## Defining Tidy Data

>Like families, tidy datasets are all alike but every messy dataset is messy in its own way.  Tidydatasets provide a standardized way to link the structure of a dataset (its physical layout)with its semantics (its meaning).

### Data Structure

##### Table 1 : Typical Presentation Dataset

|              | Treatment A | Treatment B |
| ------------ | ----------- | ----------- |
| John Smith   | -           | 2           |
| Jane Doe     | 16          | 11          |
| Mary Johnson | 3           | 1           |

##### Table 2: The Same data as in [Table1](#Table 1 : Typical Presentation Dataset) but structured differently

|             | John Smith | Jane Doe | Mary Johnson |
| ----------- | ---------- | -------- | ------------ |
| Treatment A | -          | 16       | 3            |
| Treatment B | 2          | 11       | 1            |

There are many ways to display the datasets in the table, but in order to determine which is the best for our general purpose, we need to understand the structure of the datasets. In order to understand the structure, we need to clarify the definition of **variables** and **observations**

### Data Semantics

A dataset is collection of **values**, either **quantitative(int, float)** or **strings(Could be numerical)**. Values are organized in two ways.

1. 

### Tidy Data



## Tidying Messy Datasets

### Column headers are values, not variable names

### Multiple Variables Stored in one column

### Variables are stored in both rows and columns

### Multiple types in one table

### One type in multiple tables



## Tidy Tools

### Manipulation

### Visualization

### Modeling