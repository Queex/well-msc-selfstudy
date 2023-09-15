# Introduction to R

*Suggested prerequsite courses:* ***Introduction to the Command Line***, ***Programming Concepts***.

This short course is designed to teach the basics of the *R* statistical programming language.

It does not assume any previous knowledge of programming languages, so feel free to skim through any sections that you already know. It's useful to have at least some knowledge of the command line (as R is primarily a command line-driven language), but you don't need to be experienced with the command line to learn R.

As with the other courses in this collection, you're not expected to learn everything at first glance! The goal is to give you enough familiarity with R and its capabilities that when you come to use it you don't feel completely at sea, and know how to find the information you need to complete the task you need to. As with all programming languages, learning by doing is an important and getting practice with the language is what builds skills.

## What is R?

R is a *high-level, interpreted* programming language. *High-level* means the syntax is designed to be clear for humans to read (as far as any programming language can be) rather than close to what the computer understands. *Interpreted* means there is no intermediate step where your code is *compiled* into something the computer understands, as this is done when you run your code.

R is a statistical programming language, which means it has more emphasis on powerful tools for *analysis*, *modelling* and *graphing* than a general purpose language, and less support for user interfaces and interoperability with hardware. It's core capabilities can be greatly expanded upon through the use of third-party *libraries*, the two main repositories of which are **CRAN** (the Comprehensive R Archive Network) and **Bioconductor** (for packages that specifically handle genomic data).

For the curious, R:

- Is dynamically-typed with duck typing
- Supports procedural programming
- Supports object oriented programming
- Supports meta-programming with multiple despatch

Don't worry if this means nothing to you, it's just to keep the nerds paying attention.

## Why use R?

As a programming language, R has its quirks and they can be frustrating and off-putting. Its error messages are seldom very informative, its syntax sometimes makes it awkward to understand even fairly simple code, and its help files are better at describing the intricacies of a function than they are at pointing you towards the function you need. If you run into any of these problems, you are not alone! Even very experienced R programmers run afoul of them, too.

Where R excels is in its collection of tools for **analysing data**, and in presenting that data in **publication-quality graphs**. This is hardly surprising, as those are what it was built for. Where in other languages you would need to find a third-party library to do those things, or write quite complicated code of your own, in R you can do those tasks far more easily.

The *Bioconductor* repository provides libraries that have become the de facto standard for analysing many different kinds of genomic data. If you are working with these types of data, it is almost always quicker and more convenient to work in R than in another statistical computing language.

## Where Can You Get R?

R is **open source software**, available from [cran.r-project.org](https://cran.r-project.org). Versions are available for Windows, MacOS and Linux systems. However, R is also available through Linux package managers, which simplify installing and updating R.

R is, at its heart, a command line driven language and the default interface reflects that. When you run R, you are presented with an interface wrapped around that command line. The default Windows environment is a window-of-windows application, which opens with one internal window for the command line. Other windows will open inside the main one to show plots, editing functions and help files. On Linux, R is generally run from the terminal, and as such the standard prompt is replaced by R's own prompt `>`.

However, there are options for prettier and more functional interfaces.

Many IDEs (integrated developer environments) support R code, although sometimes this requires installing add-ons. Even when the IDE understands R syntax, you will probably need to download R separately in order to run that code. **R Studio** is an IDE created specifically for working with R, and is recommended if you want the convenience of an IDE and do not already have a preferred one you use.

There are also tools that allow you to integrate R code (and other programming languages) with written text in a single document. **Jupyter Notebook** is one example. These tools work by marking certain parts of the document as code in a specific language, and offer a reasonable compromise between seeing the live results of your R code and keeping code and non-code together.

Regular R users tend to stick with whichever solution they feel most comfortable and productive using. This is fine, because the code itself does not rely on any features of an IDE or equivalent to run properly, only R itself. The code you wrote for a Jupyter Notebook document can be copy-pasted into someone else's base R command line and run just fine (assuming they have installed any libraries your code needs).

## Download and Install R

For the rest of this course, it is best to try out commands yourself, and experiment with R's commands to get a feel for it.

R might be already be installed on your computer already. If not, you can download it from [cran.r-project.org](https://cran.r-project.org).

For Linux systems, a user with root permissions can install it with:

`$ sudo apt install r-base`

or

`$ sudo yum install R`

Depending on the package manager.

## Learn By Doing!

The easiest way to get a feel for R, or any programming language, is to start messing about with it. The examples in the following sections demonstrate specific features, but it's a clever idea to try your own as you work through the examples. "I wonder what will happen if I do this..." is a good state of mind to have. No-one is going to scold you for generating an error!

#### Recap Questions

todo...