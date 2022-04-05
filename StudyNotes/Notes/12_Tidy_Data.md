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

A dataset is collection of **values**, either **quantitative(int, float)** or **strings(Could be numerical)**. Values are organized in two ways. Every value belongs to a variable and an observation. A variable contains all values that measure the same underlying attribute (like height, temperature, duration) across units. An observation contains all values measured on the same unit (like a person, or a day, or a race) across attributes.

### Tidy Data

Tidy data is a standard way of mapping the meaning of a data to it's structure. A tidy structure is as follows:

1. Each *Variable* forms a *column*
2. Each *Observation* forms a *row*
3. Each type of *observation* unit forms a *table*



## Tidying Messy Datasets

Real datasets can, and often do, violate the three precepts of tidy data in almost every way imaginable. The following Sections proposes solutions for the five most common problems with messy datasets.

### Column headers are values, not variable names



### Multiple Variables Stored in one column

### Variables are stored in both rows and columns

### Multiple types in one table

### One type in multiple tables



## Tidy Tools

### Manipulation

### Visualization

### Modeling