# Introduction to R - Vectors

### Vectors

Earlier, it was mentioned that R deals primarily in vectors of numbers. Many R functions return such vectors. Returning to our earlier example:

```
> runif(20)
 [1] 0.6966319 0.7553330 0.3658508 0.8543675 0.9656744 0.9619001 0.9688776
 [8] 0.9929829 0.2147957 0.5503601 0.3625057 0.3180858 0.5312057 0.3537757
[15] 0.3000255 0.6990726 0.3367063 0.3624072 0.7840367 0.4423911
```

In this case we tell it to generate 20 random numbers. The output overflows one line and is wrapped across three. The numbers at the start of the line tell you what the index is for the first number in that row.

*Note: Be aware that in R, unlike in most programming languages, arrays start at index 1, not index 0.*

A common situation is to generate a vector of numbers following a sequence. R has a function for that, too:

```
> seq(from=1, to=49, by=2)
 [1]  1  3  5  7  9 11 13 15 17 19 21 23 25 27 29 31 33 35 37 39 41 43 45 47 49
> seq(from=1, to=49, length.out=25)
 [1]  1  3  5  7  9 11 13 15 17 19 21 23 25 27 29 31 33 35 37 39 41 43 45 47 49
```

In the first example, we give the first and last numbers in the sequence, and the increase at each step. In the second example, with replace the last argument with the length of the vector we want returned. Both examples produce the same sequence.

If you want to create a vector by hand, you can use the `c()` function (which stands for 'combine').

```
> x <- c(1, 3, 5, 7, 9)
> x
[1] 1 3 5 7 9
```

For simple sequences, there's a useful shorthand using the colon operator:

```
> 1:10
 [1]  1  2  3  4  5  6  7  8  9 10
```

#### Vectors and Indices

To get a specific elements from a vector, you can use the square bracket notation, as is common in programming languages. Using the `x` object we created above:

```
> x[3]
[1] 5
```

However, because R is all about vectors, we can put a vector inside the square brackets and it will select only those elements from the vector.

```
> x[c(1, 2, 4)]
[1] 1 3 7
```

This command extracts the 1st, 2nd and 4th elements of the vector `x`, which are 1, 3 and 7.

Many functions operate on vectors in order to do certain tasks in parallel. Leveraging R's approach to vectors is an important part of using the language effectively.

#### Alternative Indices

Some R objects have named elements; for example the columns of a table of data. When using R's `[]` indexing, you can use names, where they exist, instead of numerical indices.

```
> y <- 1:5
> names(y) <- c("a","b","c","d","e")
> y
a b c d e 
1 2 3 4 5 
> y["a"]
a 
1 
```



#### Vectors and Operators

R can perform arithmetic on vectors (and matrices, which we won't cover here), but it doesn't follow the mathematical rules of matrix arithmetic. Instead, it performs the operation pairwise on elements in the vectors in sequence.

```
> 1:5 + 2:6
[1]  3  5  7  9 11
> 1:5 * 2:6
[1]  2  6 12 20 30
```

If the vectors are not of the same length, then the shorter one will be repeated.

```
> 1:6 + 1:2
[1] 2 4 4 6 6 8
```

In this example, the second vector is repeated three times to match the length of the first.

If the length of the longer vector is not a multple of the length of the shorter vector, R will still do the repeat but will raise a warning.

```
> 1:5 + 1:2
[1] 2 4 4 6 6
Warning message:
In 1:5 + 1:2 :
  longer object length is not a multiple of shorter object length
```

The warning does not stop R from producing output.

**Because R will never give an error for these types of length mismatches, they are a common cause of difficult to diagnose bugs.**

In the special case where one of the vectors is of length one, then that value is recycled for the length of the longer vector.

```
> 1:5 + 2
[1] 3 4 5 6 7
```

### More About Assignment


