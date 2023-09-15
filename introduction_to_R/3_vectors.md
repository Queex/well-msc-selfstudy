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

In the special case where one of the vectors is of length one, then that value is repeated for the length of the longer vector.

```
> 1:5 + 2
[1] 3 4 5 6 7
```

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

You can also use logical values as indices. In this case, `TRUE` is interpreted to mean include the element in the output, and `FALSE` to not include it. The logical vector used as the index will be repeated if necessary, to the full length of the vector.

```
> y[c(TRUE, FALSE)]
a c e 
1 3 5 
```

#### Vectors and Comparators

Comparators, like other operators in R, consider vectors element by element. This means that `==` and `<` and the others might not behave how you would expect:

```
> c(1, 1) == c(1, 2)
[1]  TRUE FALSE
> c(1, 1) < c(1, 2)
[1] FALSE  TRUE
```

There are two functions it's useful to know about that take a vector of `TRUE` and `FLASE` values as their argument: `any()` and `all()`.

```
> all(c(TRUE, FALSE, TRUE))
[1] FALSE
> all(c(TRUE, TRUE, TRUE))
[1] TRUE
> any(c(TRUE, FALSE, FALSE))
[1] TRUE
> any(c(FALSE, FALSE, FALSE))
[1] FALSE
```

As you can see, they each turn a logical vector into a single value, with the value intuitive to their names.

When you want to compare two vectors and make sure they are the same, there's a more direct function that does what you need:

```
> identical(c(1, 1, 3), c(1, 2, 3))
[1] FALSE
> identical(c(1, 2, 3), c(1, 2, 3))
[1] TRUE
```

There is a subtle trap you can fall into if using `all()` to replicate `identical()`:

```
> all(c(1, 2, 1, 2) == c(1, 2))
[1] TRUE
> identical(c(1, 2, 1, 2), c(1, 2))
[1] FALSE
```

R's habit of repeating vectors comes to ruin your day again! `identical()` is a stronger test because it also checks the length of the two vectors. It actually also compares data types (which we'll get to later) and is the preferred way to check that two objects or expressions are, well, identical. This family of functions, that compare vectors and return a single logical value, are particularly handy when used in combination with the `if()` statement, which expects a single logical value.

You might be wondering how you can test if a value is in a vector. R's tool for this is a special operator: `%in%`.

```
> 1 %in% c(1, 2, 3)
[1] TRUE
```

Of course, this operator can also be used with a vector on the left hand side. The result in that case is a vector, of the same length as the left hand side, with a `TRUE` value for each element that was present in the vector on the right hand side.

```
> c(1, 3, 5, 7) %in% c(1, 2, 3)
[1]  TRUE  TRUE FALSE FALSE
```

#### Vectors and Logical Operators

R's primary operators for 'and' and 'or', `&` and `|`, also consider vectors element by element. This is very useful for tasks like checking a vector for multiple conditions:

```
> y <- c(1, 2, 3, 4, 5, 6)
> y < 5 & y > 2
[1] FALSE FALSE  TRUE  TRUE FALSE FALSE
```

If you're familiar with other programming languages, you are probably aware of the idea of 'shortcut and' and 'shortcut or'. These differ from the regular kind by stopping and returning once they know what the final result will be. If the left hand side of a shortcut and is False, then it doesn't need to check the right hand side. The shortcut versions are the most commonly-used version in most programming languages. However, in R, where you're dealing primarily with vectors, they are less useful.

Worse, in R, these shortcut operators will *ignore* every element of a vector except the first, and do so completely silently. This can be the source of very frustrating errors.

```
> y < 5 && y > 2
[1] FALSE
```

#### Vectors and Assignment

R's approach to vecotrs and indices also extends to assignment. You've already created a vector with a single assignment statement. Like most programming languages, you can also assign to specific elements in a vector.

```
> x[2] <- 2
> x
[1] 1 2 5 7 9
```

R also allows you to assign to multiple elements at once in a similar way:

```
> x[4:5] <- c(1,2)
> x
[1] 1 2 5 1 2
```

In fact, when you do this, the indices you assign to do not even have to be grouped together. You can even combine several of the principles above into a line like:

```
> x[x == 1] <- 9
> x
[1] 9 2 5 9 2
```

The `x == 1` part produces a logical vector, which is `TRUE` when that element of `x` equals 1. Using a logical vector as an index means R will only look at those positions in the vector. And because this is an assignment, only those values will get changed. What they get changed to is a vector of length 1 (i.e. a number), which is repeated as much as is needed to match the number of elements that are being assigned to.

At this point, you might understand why R is sometimes considered something of an oddity among programming languages.

#### For Loops

Another important programming idea is that of a for loop. A for loop allow you you perform the same (or similar) task over a vector of values. It's easiest to see an example:

```
> y <- 1:20
> z <- 0
> for(i in y){
+   if(i > 10){
+     z <- z + 1
+   }
+ }
> z
```

The variable `z` starts at zero, and is increased by one for each element of `y` that's greater than 10. R's `for()` syntax requires a variable for the loop, in this case `i`, and a vector of values for that variable to take. In this example, that vector was the sequence `1:20`, but it can be any vector. Then the curly brackets enclose the block of code that will be run at each iteration.

The key idea is that the block is run once for each value that `i` takes.

Although for loops exist in R, you will seldom encounter them because R's vector-centric approach means they are usually unnecessary. If you compare this for loop example to the last example for assignment, above, you can probably intuit how there's a simper way to calculate the intended `z`.

```
> y <- 1:20
> z <- y > 10
> z
 [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
[13]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
> z <- length(z[z == TRUE])
> z
[1] 10
```

The interim value of `z` is shown for clarity. The expression `z[z == TRUE]` shows only the `TRUE` elements of `z`. We can then use the `length()` function, which does exactly what you expect, to find how many elements of `y` were greater than 10.

There is actually an even quicker (and sneakier) way of performing this task, which we'll come back to later.

### Recap Questions

todo...