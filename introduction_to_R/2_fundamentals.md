# Introduction to R - Fundamentals

## The R Console

The command line interface for R shares a lot of its behaviour and shortcuts with other command line interfaces, including:

- Up and down arrows to scroll through the history of commands entered
- *Control+C* to halt the current command (although in the default Windows interface you need to use *Escape*, but there is also a 'Stop' button in the interface)
- Pressing *Tab* to complete command names and files
- A *working directory* where your R session is based. If you start R from the command line, this will be the same directory you were in for the command prompt. If you start R from the operating system, this will usually be your user directory (`~`) or (`%USERPROFILE%`).

R has three different ways to show output on the console.

- When it prints output normally, it is prefaced with a decorator similar to `[1]`. This is because R works with *vectors*, or arrays of values, which can wrap over many lines of output in its interface. This decorator lets you know the index of the first entry on that particular line, to make it easier to count along if you need to. This output is only printed when R has completely finished the command it was running.
- R can also print any text while it is running a command. This is usually done to show progress when running a command that takes a while to execute.
- When R encounters an error, it prints the error message. With some interfaces this message is in a different colour to other output, to help differentiate it.

## R Objects and Sessions

R primarily works on data held in memory, rather than reading that data from files. Each piece of data is called an **object**, in R's parlance, and is given a unique name. These objects behave like variables, that you can refer to in your code by their names. Once an object is stored like this, it stays there until you explicitly remove it. This means that your R session can become clogged with objects you intended to be temporary. R has a function to remove objects you no longer need, but take care not to accidentally remove data you still need!

As some of the data sets R is used for are very large, it's possible to run into difficulty by running out of memory. This is actually most likely to happen when using a computing cluster, as by default the memory assigned to jobs on clusters is usually lower than the memory available on a desktop or laptop system. On personal computers running out of memory usually results in the computer slowing down considerably as it swaps data back and forth between memory and the hard drive continuously.

When you quit R, it will ask you if you want to save your current session. What this means is that the objects in memory are stored all together in a special `.RData` file, in a format particular to R. It also creates a `.RHistory` file, containing the command history. These will both be saved in R's current *working directory*. If you start R from that directory, it will automatically load both files, restoring all your objects and command history. This allows you to pick up more-or-less exactly where you left off.

This also means that you can organise different projects into different working directories, keeping the data and history separate for each one.

## Basic R Commands

### Arithmetic

You can, if you want, use R as a calculator.

```
> 3 + 4
[1] 7
```

The `>` is R's prompt. `3 + 4` is what you typed. `[1] 7` is R's output. For a simple sum like this, the output is a single value, but R still uses its vector notation `[1]` before the output.

R uses a number of usual operators:

| Symbol | Use |
|---|---|
| `+` | addition |
| `-` | subtraction |
| `*` | multiplication |
| `/` | division |
| `^` | exponentiation |
| `%%` | modulus |
| `%/%` | integer division |
| `==` | equal to |
| `<`, `<=`, `>`, `>=` | comparators |
| `!=` | not equal to |
| `&` | 'and' operator |
| `|` | 'or' operator |


*Note: You don't strictly need to put spaces between operators and numbers, but it makes you code easier to read.*

### Creating Objects

To create an object in R, you assign a value to a name like this:

`> x <- 7`

`<-` is a special operator in R used to assign values. Other programming languages usually use `=`. You can also use `=` in R, and it will do the same as `<-`, but it's recommended to use the `<-` version to avoid any potential confusion with the equality operator `==`.

*Note: You might notice that R gives no output after the above command. R does not return any output from an assignment.*

`x` is now an object in what R calls its 'store'. You can now use `x` as a variable in other commands:

```
> x
[1] 7
> x + 4
[1] 11
> x * 1.5
[1] 10.5
```

The object `x` will only change value if you assign a different value to it.

```
> x <- x * 1.5
> x
[1] 10.5
> x <- 11
> x
[1] 11
```

#### Managing Objects

You can see what objects you have created with the `ls()` function (we'll talk about functions in more detail a little later):

```
> ls()
[1] "x"
```

You can remove objects using the `rm()` function:

```
> y <- 12
> ls()
[1] "x" "y"
> rm(y)
> ls()
[1] "x"
```

Some interfaces that wrap around R allow you to see the object store in real time, including inspecting specific objects to view their contents.

#### More On Object Names

The names of R's objects are case sensitive. That means you will see the following if you capitalise `X`:

```
> X 
Error: object 'X' not found
```

Object names in R cannot contain spaces or hyphens (`-`), but you can use underscores (`_`) and full stops (`.`). If you are loading data into R from a file, a common source of problems is data containing spaces or hyphens. R will attempt to fix invalid names by replacing problem characters with `.`, but this can cause knock-on problems when those names don't match something that wasn't corrected in that way. It's generally best to make sure that the data file doesn't use any forbidden characters before trying to load it into R.

Object names can contain numbers, as long as the name does not start with a number.

You cannot create two objects with the same name. If you try, you will over-write the first.

You *can* create objects with the same name as existing R functions, but you should avoid doing so. You cannot create objects with the name name as one of R's special keywords.

### The Continuation Prompt

In most command line languages, if you leave a command unfinished you will get an error. R, however, can detect some instances of this and will give you a different prompt: `+`. This is the continuation prompt, and you can finish typing your command on that next line. R will join the lines together when it tries to execute it.

```
> x <-
+ 11
> x
[1] 11
```

While this is often useful to help write code that spans multiple lines, sometimes you will see that your mistake was earlier in the line, and you can't fix the mistake just by adding more to the end of the line. You can use *Control+C* or *Escape* to break out of the continuation prompt and get back to the regular one.

### Functions

R comes with a wide variety of functions, for mathematical and statistical operations. To call an R function, you use the function name and round brackets (`(`, `)`). The arguments to the function go inside the brackets, separated by commas. R functions support both **default arguments** and **named arguments**. Many of R's core functions have many, many possible arguments, and it would be impractical to have to type them all out.

An example of using an R function is:

```
> runif(1)
[1] 0.03999256
```

This has generated a random number from a uniform distribution. The argument 1 says how many numbers to generate. The function has two other arguments with default arguments, for the minimum and maximum values the random number can take. We can change those from the default values by adding arguments:

```
> runif(1, 0.25, 0.5)
[1] 0.3332207
> runif(1, max=0.5, min=0.25)
[1] 0.3211315
```

Note that both of these commands are using the same uniform distribution, between 0.25 and 0.5. In the first example, we give the argument in the order the function expects. in the second, we use named arguments to set them so we don't have to worry about the correct order.

At this point, you may be wondering how you know what order the arugments need to be, or what they are named. This where the `help` function comes in.

#### The Help Function

You can use the function:

`> help(runif)`

To look at R's help file for the function we used above. This will either open the html help file in a new browser window or show the help file in a command line text viewer (depending on how you are running R).

R help files are, unfortauntely, something of a mixed bag. They tend to be very thorough with respect to details, but aren't so good at explaining the context a function is meant to be used in. They are also not very useful when you know *what* you want to do, but you don't know where to start looking. In those cases, a web search will probably be more informative.

You can also look at the help for a function using this short-hand:

`> ?runif`

You can perform a fuzzy search using a double question mark:

`> ??runif`

#### Creating Your Own Functions

You can write your own functions in R. These are treated as objects, stored alongside data, with names that follow the same rules. Although it's possible to write them using R's command line interface it's more convenient to write them in a text editor or IDE and then load them into R. Creating a function in R looks like this:

```
my_exp_function <- function(arg1, arg2=10){
    out <- arg2 ^ arg1
    return(out)
}
```

(This is shown as it would appear in a script, without prompts)

The `my_exp_function <-` part is assigning the function to that name, as you would with a data object.

`function` is an R function, used to create a function, and it's hopefully not as confusing to understand as it was to type out.

Inside the round brackets are the argument names that the function will use. The second one is given a default value of 10 (using `=`; which is the only part of standard R code style where you should use `=`).

The curly brackets (`{`, `}`) contain the code block for the function itself. Inside that block are valid lines of R code, which are executed one by one when the function is called.

`return(out)` is a special function that it used to give the return value of a function. You can only return one value, and lines of code after this return function would be ignored.

We create an object inside this function. Objects created inside functions in this way are discarded after the function completes.

### Logic and If Statements

The comparison and equality operators in R do not result in number but in logical values. In R, these are represented by the special values `TRUE` and `FALSE`. They can abbreviated as `T` and `F`.

```
> 2 < 3
[1] TRUE
```

The table earlier gives you two logical operators: `&` for 'and' and `|` for 'or'.

#### If Statements

As in many programming languages, you may need to write code that is only executed when certain conditions are met. The structure that R uses looks like this:

```
> if(x > 10) {
+   "Big"
+ } else {
+   "Small"
+ }
[1] "Big"
```

Here we are taking advantage of the continuation prompt to write this over multiple lines so it's easier to read.

The keyword `if` kicks things off. Inside the round brackets there must be an expression that evaluates to a single logical value. In the next section we will discuss how to use R's vectors, but this part of an `if` statement is one place where you must have only a single value.

If that expression evaluates to `TRUE`, then the code inside the curly brackets will be run. Otherwise, it will not.

The follow-up keyword `else` marks a second block, which will be run when the condition evaluates to `FALSE`.

#### Recap Questions

todo...
