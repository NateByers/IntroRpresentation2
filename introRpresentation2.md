Learning R, Part 2
========================================================
author: Nathan Byers
date: April 21, 2014

Beyond basics
========================================================

Now that we <a href="http://rpubs.com/NateByers/introR" target="_blank">know some basics</a>, we'll cover

- importing data from a spreadsheet
- data types
- functions

Importing data
========================================================
type: section

Importing data
========================================================

- Probably the most common format for data storage is Excel
- Unfortunately, you can't import Excel files with base R
- There _are_ <a href="http://cran.r-project.org/doc/manuals/r-release/R-data.html#Reading-Excel-spreadsheets" target="_blank">packages</a> that will do it 
- But the best way to import spreadsheet data is to use the CSV file format


Starting with Excel
=========================================================

- First, open your Excel file
- Go to "Save As"
- For the "Save as type" option, select "CSV (Comma delimited)"
- You'll only be able to save one sheet (CSV won't support multiple sheets)


Read in the file
========================================================

- Let's say you named the file "mydata.csv" in a folder called "Documents" in your C: drive
- In R, use the following code

```r
data <- read.csv(file = "C:/Documents/mydata.csv")
```

- R will assume that the cells in the first row of your spreadsheet contain column headers
- The variable `data` will be a data frame

Data types
==========================================================
type: section

Data types
========================================================

- We'll cover the following data types in R (some of which we touched on in part 1)
 - vectors
 - matrices
 - data frames
 - lists

Vectors
========================================================
type: type: sub-section

- Vectors are variables with ordered, or indexed, values
- All of the values in a vector must be the same class
- Some basic data classes in R are character, integer, numeric, and logical

Vectors
========================================================

Class | Example
------|--------
character | `c("red", "white", "blue")`
integer | `c(1, 2, 3)`
numeric | `c(1.5, 2.9, 3.3)`
logical | `c(TRUE, FALSE, TRUE)`

Vectors
========================================================
- To retrieve a value using the index of a vector we use brackets
- Here we create a vector of character values and retrieve the 2nd value

```r
x <- c("red", "white", "blue")
x[2]
```

```
[1] "white"
```



Matrices
========================================================
type: type: sub-section

- A matrix is a rectangular array of values
- In R, all values in a matrix must be of the same class
- So, you can have a matrix of numbers or a matrix of characters, but not both
- If you mix them, R will convert all values in the matrix to the most general class, which would be character

Matrices
=========================================================
- Below we create a matrix using the `matrix()` function
- We use the colon to create an ordered sequence (e.g., `1:3` creates the vector `c(1, 2, 3)`)

```r
m <- matrix(data = 1:12, nrow = 3)
m
```

```
     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12
```


Matrices
========================================================
- We use brackets to retrieve a value, or a subset of values, `[rows, columns]`
- Here, we retrieve the first column of the matrix from the previous slide

```r
m[, 1]
```

```
[1] 1 2 3
```


Matrices
=======================================================
- Here we retrieve the second row of the matrix

```r
m[2, ]
```

```
[1]  2  5  8 11
```

- And here we select the value in the 3rd row, 4th column

```r
m[3, 4]
```

```
[1] 12
```


Matrices
=======================================================
- To select more than one row or column, use vectors for rows and columns
- Here we select the 4 values in the lower right hand corner of the matrix

```r
m[c(2, 3), c(3, 4)]
```

```
     [,1] [,2]
[1,]    8   11
[2,]    9   12
```


Data frames
========================================================
type: type: sub-section
 
- Data frames are like matrices, but the difference is that all of the values don't have to have the same class
- You can think of a column of a data frame as a vector with a certain class
- The main restriction is that each column has to be the same length as all the others

Data frames
=========================================================

Here's the example from part 1:


```r
price <- c(1000, 4000, 2000, 5000, 500)
carat <- c(0.4, 0.55, 0.45, 0.65, .2)
color <- c("G", "H", "D", "E", "G")
diamonds <- data.frame(price, carat, color)
diamonds
```

```
  price carat color
1  1000  0.40     G
2  4000  0.55     H
3  2000  0.45     D
4  5000  0.65     E
5   500  0.20     G
```


Data frames
==========================================================
- Like with matrices, we use brackets to retrieve values or subsets
- Here we get the last two prices from the `diamonds` data frame

```r
diamonds[c(4, 5), 1]
```

```
[1] 5000  500
```


Data frames
==========================================================
- When columns (or rows) have names, we can use those instead of numbers

```r
diamonds[c(4, 5), "price"]
```

```
[1] 5000  500
```


Data frames
==========================================================
- And to get a column, we can also use the `$` symbol

```r
diamonds$price
```

```
[1] 1000 4000 2000 5000  500
```


Lists
==========================================================
type: type: sub-section

- Our last data type is the list
- It's like a vector, but each "value" in a list is not restricted to one number or character string
- A member of a list can be a vector, a matrix, a data frame, or even another list

Lists
===========================================================

- Lists are handy because you can create a data object that isn't restricted to the table format
- For example, we could create an object that contains the diamonds data frame along with some other information


```r
sales <- list(product = diamonds, store = "downtown", month = "january")
sales
```


Lists (output)
===========================================================


```
$product
  price carat color
1  1000  0.40     G
2  4000  0.55     H
3  2000  0.45     D
4  5000  0.65     E
5   500  0.20     G

$store
[1] "downtown"

$month
[1] "january"
```


Functions
============================================================
type: section


Functions
=============================================================

- Functions have the form `function()` and take arguments in the parenthesis
- If you want to know what arguments are required for a function to work, type
a question mark in front of it and run it
- In RStudio, the helpfile will appear in the bottom right panel



Functions
============================================================
- For example, to see the help file for the `matrix()` function, run

```r
?matrix()
```


- You can see that the arguments for `matrix()` are `data`, `nrow`, `ncol`, `byrow`, and `dimnames`

***

![alt text](figures/matrixHelp.png)

Functions
===========================================================
- The help file gives more specific details on each argument

![alt text](figures/matrixHelp2.png)

Functions
===========================================================
- You can specify each argument when you run the function, or you can supply the argument in the order
they appear in the help file

```r
matrix(data = 1:12, nrow = 3)
```

is equivalent to 

```r
matrix(1:12, 3)
```


Part 3
==========================================================
- <a href="http://rpubs.com/NateByers/introR3" target="_blank">Part 3</a> of this series explains how to write your own functions, as well as a few more advanced topics
- These presentations were created using RStudio's <a href="http://www.rstudio.com/ide/docs/presentations/overview?version=0.98.501&mode=desktop" target="_blank">"R Presentations"</a>
- The code for this presentation can be found here: <a href="https://github.com/NateByers/IntroRpresentation2" target="_blank"> https://github.com/NateByers/IntroRpresentation2</a>


