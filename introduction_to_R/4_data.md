# Introduction to R - Data

## Data Types

We've already seen 'numeric' and 'logical' values in R, but what other flavours of data might you encounter?

### Character

Some of the examples seen earlier used a text string. In R, this is called a 'character' data type. When using this data type, you should enclose the text in double quotes (`"`). Mathematical operations cannot be performed on character data, of course.

```
> "3" + 2
Error in "3" + 2 : non-numeric argument to binary operator
```

When you need to specify files, you do so using the character data type. R has a very useful feature for this, where tab completion can be used to find and complete file paths when you're typing inside `"` symbols. If you type:

`> "~/`

and then hit the *Tab* key, R will show you a (partial) list of files in your home directory. You can start typing the name of a file and use *Tab* to complete it, saving much time and error when working with files.

(Remember to use *Control+C* or *Escape* to break out of that partial line when you're done!)

### Integer

Integer is almost identical to numeric. The difference is behind the scenes, related to how computers store number of different types. R will normally only use the integer data type when you specifically convert to it, preferring the more general numeric type for numbers you type. For your R code, it will not make a difference.

### Factor

Factor data is, in essence, a special kind of character data. Whereas a character vector can contain any string, a factor is defined as having only a specific set of allowed values, called in R 'levels'. This is implemented behind the scenes by making the data value an integer, but attaching a look-up table from those integers to the character value. This is more memory-efficient than storing the full character string for each occurrence.

```
> z <- factor(c("a", "b", "c", "a"))
> z
[1] a b c a
Levels: a b c
```

The `factor()` function is one way to create factor data. You can see the data doesn't get displayed with enclosing `"`, here, because it is factor data not character data. Underneath the vector, R reports what levels exist for that factor.

Factors are mostly encountered when dealing with large tables of data, or with particular statistical models. Tables are covered later in this section.

If we try to change one of the elements of a factor vector to an invalid string, we get a warning:

```
> z[4] <- "d"
Warning message:
In `[<-.factor`(`*tmp*`, 4, value = "d") :
  invalid factor level, NA generated
```

The last line is the salient part, telling us about an invalid factor level. Care must be taken when using factors, to make sure you only try to assign allowed factor values.

### NA

R has a special data value, called `NA`. This represents data that is 'not available', and can crop up in a number of ways related to missing data, or numerical errors. It has special behaviour that might puzzle you at first:

```
> NA == NA
[1] NA
```

You might have expected to see `TRUE`. The actual behaviour makes sense if you consider that `NA` is meant to be a place-holder for something missing, or incorrect. Any operator will return `NA` if at leat one of its operands is `NA`. Otherwise, you might have a test like `x != 0` and become confused that the value is `TRUE` but the data is missing.

Although this behaviour is useful in many circumstances, the fact that your code will not automatically stop with an error when an `NA` is generated can cause problems. You might have a long, complicated block of code only to find nothing but a vector of `NA` values as the output. Tracking down where in that code the `NA` was first introduced can be difficult.

The correct way to test that a value is `NA` is using this function:

```
> is.na(NA)
[1] TRUE
```

### Determining Data Type

R has a convenient function, `class()`, that will return the class of any data object.

```
> class(3)
[1] "numeric"
> class("3")
[1] "character"
> class(factor("3"))
[1] "factor"
```

An alternative method is to use one of the functions of the `is.x` family:

```
> is.logical(TRUE)
[1] TRUE
> is.logical(3)
[1] FALSE
> is.numeric(TRUE)
[1] FALSE
> is.numeric(3)
[1] TRUE
```

Bear in mind that these functions reflect what R has *stored* the data as, not what it could be converted to:

```
> is.integer(3)
[1] FALSE
> is.numeric("3")
[1] FALSE
```

In the first case, although 3 is clearly an integer, R defaults to the numeric type for all numbers unless otherwise specified.

### Changing Data Type

In some circumstances, R will change the data type by itself. If you perform certain operations and functions on different data types, R will change the overall data type to the most general one. If you attempt to mix data types, then R will convert the entire vector to a more general data type.

```
> c(1, 2, "three")
[1] "1"     "2"     "three"
```

Character data is considered the most general data type.

You can also change to a type using one of the `as.x` family of functions:

```
> as.integer(3)
[1] 3
> as.character(3)
[1] "3"
> as.factor(3)
[1] 3
Levels: 3
> as.logical(3)
[1] TRUE
```

Wait, the first three examples make perfect sense, but what's going on with the fourth? Well, programming languages like to be able to convert between numbers and logical values, and R is no exception. In R, `0` converts to `FALSE`, and any other number converts to `TRUE`. Similarly, in the other direction, `FALSE` converts to `0`, and `TRUE` converts to `1`. This leads to a simpler version of the 'greater than 10' example in the previous section:

```
> y <- 1:20
> sum(y > 10)
[1] 10
```

`y > 10` returns a vector of logical values, and the `sum()` function adds all the elements of a vector. R converts the logical vector to a numeric one, converting all the `TRUE` values to `1` and all the `FALSE` values to `0`, then finds that sum to get the answer we wanted.

Converting factor data requires special care.

```
> z <- factor(c("a", "b", "c", "a"))
> c(z, "a")
[1] "1" "2" "3" "1" "a"
```

This might seem like a very strange result, and it is. What has happened is that the `"a"` we are using in the `c()` function is a character, not a factor. Therefore R converts `z` to a character to match it. However, instead of doing this the way you might expect, it first converts is to a numeric vector, revealing the numbers for the look-up table, then converts *that* to a character vector.

One way to achieve what we were trying to do is to force R to convert `z` to a character vector in one jump, then turning the larger vector back into a factor.

```
> factor(c(as.character(z), "a"))
[1] a b c a a
Levels: a b c
```

## Data Structures

We've talked a lot about using vectors, but R also has other ways of storing data. In computer science lingo, these are called 'data structures', and some of the ones in R are covered below.

### Matrices

A matrix is an obvious extension of the idea of a vector. Matrices in R are treated a little bit like a special kind of vector; just with an extra attribute that says how long the columns are. This means that they behave very similarly to vectors, including how they behave with respect to R's operators. There is a `matrix()` function that creates a matrix from a vector:

```
> z <- matrix(1:25,nrow=5)
> z
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    6   11   16   21
[2,]    2    7   12   17   22
[3,]    3    8   13   18   23
[4,]    4    9   14   19   24
[5,]    5   10   15   20   25
```

The `1:25` expression forms the content of the matrix, and R fills its matrices column by column, top to bottom. You can use `nrow` to say how many rows, or `ncol` to say how many columns, or both.

As you may have guessed from the deocrators around the matrix in the output, R uses the same square brackets for matrices as it does for vectors, just with two indices. The first index in R refers to the row, the second to the column.

```
> z[1,4]
[1] 16
```

If you leave one of those positions blank, R will assume you want everything that matches the other index.

```
> z[1,]
[1]  1  6 11 16 21
> z[,4]
[1] 16 17 18 19 20
> z[,]
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    6   11   16   21
[2,]    2    7   12   17   22
[3,]    3    8   13   18   23
[4,]    4    9   14   19   24
[5,]    5   10   15   20   25
```

Notice that when you extract a single row or column, R will convert it into a single vector, regardless of the original orientation. For 'real' vector and matrix mathematics, you need to use special functions and operators (`%*%` for matrix multiplcation, `%o%` for the outer product of two vectors, and others).

You can name the rows and column of a matrix, as you can name elements of a vector. `rownames()` and `colnames()` return the current names, and you can assign to them as you did with `names()` for vectors.

However, matrices are rarely used in R because data frames, coming up soon, are more practical for the data-based applications R is most often used for.

### Lists

An R 'list' is a more flexible data structure. You can have any number of entries in a list, and each entry can be a completely different data type, or even a data structure in its own right (including another list!). One way to create a list is through the `list()` function.

```
> z <- list(1:5, 15:20, c("a", "b", "c"))
> z
[[1]]
[1] 1 2 3 4 5

[[2]]
[1] 15 16 17 18 19 20

[[3]]
[1] "a" "b" "c"
> class(z)
[1] "list"
```

As the decorators imply, you use doubled square brackets to access elements of a list.

```
> z[[1]]
[1] 1 2 3 4 5
> z[[1]][3]
[1] 3
```

The second example above demonstrates that because `z[[1]]` is a vector, you can then use vector indexing directly. This makes it relatively easy to navigate even very deep list structures.

As with vectors, you can also name list entries:

```
> names(z) <- c("one", "two", "three")
> z
$one
[1] 1 2 3 4 5

$two
[1] 15 16 17 18 19 20

$three
[1] "a" "b" "c"
```

Unlike the rows and columns of a matrix, each element of a list can be a different length. The decorators for this output hint at another feature: you can use the `$` symbol to access an element of a list by name:

```
> z$one
[1] 1 2 3 4 5
```

You can also name the entries when you create the list:

` z <- list(one=1:5, two=15:20, three=c("a", "b", "c"))`

R does some magic behind the scenes to infer that the argument names in this command, that you have just made up, are interpreted as names for the elements of the list.

### Data Frames

For tabular data, R uses a structure called a 'data frame'. This is a little like a matrix, and a little like a list. Each column of a data frame can be a different data type, like the contents of a list. The `data.frame()` function is one way to create one.

```
> z <- data.frame(alpha=1:5, beta=16:20, gamma=c("a", "b", "c", "d", "e"))
> z
  alpha beta gamma
1     1   16     a
2     2   17     b
3     3   18     c
4     4   19     d
5     5   20     e
> class(z)
[1] "data.frame"
```

You can use either matrix indexing, or list-like names to access columns.

```
> z[1,]
  alpha beta gamma
1     1   16     a
> z[,1:2]
  alpha beta
1     1   16
2     2   17
3     3   18
4     4   19
5     5   20
> z[,"gamma"]
[1] "a" "b" "c" "d" "e"
> z$gamma
[1] "a" "b" "c" "d" "e"
> class(z$gamma)
[1] "character"
```

As with matrices, when you extract a single column it will get converted into a simple vector. It will not do this for rows, however. This is because a row of a data frame might have a number of different data types, and a vector can only have one.

You can use `rownames()` and `colnames()` for data frames, as for matrices.

### Objects

'Objects' are a general term for specialised data structures in R. They are named because they are used for R's form of object-oriented programming. Some R packages define their particular objects that their functions use, and it's only worth mentnioning them here so you don't get startled by encountering such a thing when working with one of R's packages.

## Reading and Writing Data

These data types and structures are all well and good, but typing data in long hand is not practical. R has several features to import and export data in tabular format. Plain text data formats, such as those you'll encounter when using uncompressed files on the command line, are well-supported in R. R can also handle most common types of compression. However, proprietary binary data formats such as Microsoft's `.xlsx` or the open standard `.ods` are less well-supported. It's generally best to do any conversion outside R, before importing it or after exporting it.

R will import data into data frames. R can export structures other than data frames, but data frames generally work best.

### Reading Data

R has a family of functions for reading tabular data. The most general one is `read.table()`. If you look at the help for this function, you'll see a dazzling array of arguments, allowing you handle any particular text format of this type, but the three that are the most important are:

- file – This is the actual file you want to open. Remember that R has a working directory, and that is the base location it looks in when searching for files.
- header – This is a logical value that says whether the first row of the file should be interpreted as the column names. If `FALSE`, the columns will be given generic names generated by R.
- sep – This is the separator between fields in the table. Common values for this are `","` and `"\t"` (which means a tab character). The default in `read.table()` is to treat any whitespace character (spaces, tabs, new lines) as a separator.

Because it's laborious to have to define all of `read.table()`'s arguments, there are two convenient functions that handle common data formats:

- `read.csv()` – has sensible defaults for the 'comma separated values' format, which is most often found when exporting data from a spreadsheet program.
- `read.delim()` – has sensible defaults for data separated by tabs, as is most often found in data generated by command line tools. This is also sometimes called the `tab separated value` format.

### Writing Data

As you might expect, R also has a `write.table()` function. This also has a baffling large number of options, but the one that trips people up most often is:

- row.names — If this is true, then the first column of the output file will be the row names of the data frame. This is not as convenient as you might expect, because this can lead to there being a different number of entries on the first row compared to the rest of the file, because the row names don't have a column title. It's best to set this argument to `FALSE`, but make sure the data frame has a column with name information.

#### Recap Questions

todo...