# Introduction to R - Packages

## How Do R Packages Work?

R extends its core functionality through specific libraries. These add new functions and, in some cases, new syntax that extend what you can do with R. R's greatest strength is the wide selection of statistical and bioinformatical packages, many of which are the standard tools in their fields. It's just unfortunate that the process for installing and using libraries can sometimes be like pulling teeth.

R maintains a list of what it calls 'packages' as a part of its installation. A great many packages come as part of the standard R install, but you can also install additional packages created by other users. There is a centralised archive of these packages, called [CRAN](https://cran.r-project.org/), which stands for 'Comprehensive R Archive Network', where you can find most packages.

Even when a package is installed, you need to perform an additional step to actually use it. Because there are so many packages, from so many people, it's unavoidable that some of the function names will clash. Therefore, you have to specifically say which package you want to use.

### Installing Packages

The main mechanism is the function `install.packages()`. You use it in this way:

```
> install.packages("tidyverse")
```

This function will install the named package or packages onto your system – in this case, something called 'tidyverse'. As part of the process, R may also ask you to choose a 'mirror'. Each of these mirrors has the entire archive available, picking one closer to you geographically just means a slightly faster download speed (something that becomes less relevant year by year, but useful to know).

If you do not have permissions to make root/administrator changes to your system, then it will ask you if you want to install packages into a 'user' library. The only difference this makes is that other users of that computer won't have the packages installed for them. Having an administrator install them for everyone saves disk space, but surrenders some control over what versions are available.

Libraries for programming language typically have dependencies on other libraries, and R is no exception. The `install.packages()` function will, as part of its process, find and install all the dependencies for the package you requested. that's why, if you run the example given above, you will see a *lot* of activity in R as it finds and installs dependencies, and dependencies of dependencies, and so on.

Installing a package will also install any help files for it (if there are any). This means you don't have to do the step below if all you want to do is look at the help page for a function.

### Using Packages

Once a package is installed (and remember that R's core packages are always installed), you can access it by using the command:

```
> library(tidyverse)
```

The `library()` function tells R that you want to use the package you name. You might have noticed that `install.packages()` needs the package name to be in quotes (`"`), but `library()` does not. This is because once a package is installed, R can recognise its name as an object. Once you've used `library()`, the functions of that package are now available to use. Some packages will print information when you import them using `library()`. Unless there's an error, this is purely informational.

You might wonder why you don't see the functions from a package when you use `ls()` to view the objects in your session. Functions that are part of a package, and packages themselves, are hidden from that list so it doesn't become too cluttered.

Somewhat inconveniently, the list of packages you have `library()`ed is **not** preserved when you save and restore an R session. You have to remember to use `library()` again when you restart R.

### Bioconductor

In the introduction we mentioned [Bioconductor](https://www.bioconductor.org/), as a different repository of R packages. Because nothing in computing is never as simple as it should be, Bioconductor uses its own, separate method for installing packages, which you should always use in preference to the standard one for packages that are available in Bioconductor. This is because the equivalent packages in CRAN tend not to be updated as frequently, or at all. Bioconductor uses a package, *BiocManager*, to install its own packages. Because BiocManager is, itself, also an R package, you have to install it from CRAN first.

```
install.packages("BiocManager")
```

Once this is done, you can install specific Bioconductor packages using a command like this:

```
BiocManager::install("GRanges")
```

(The `::` operator here is R's syntax for using a function from a package without going to the trouble of using `library()` on that package.)

Once you've installed packages using Bioconductor, you still need to use `library()` to make them available.

### This Doesn't Sound So Bad

Although both of these processes are simple, in principle, they are both fragile. Packages can be very picky about what versions of their dependencies they will accept, and also what version of R they will accept. If you accidentally got a Bioconductor package from CRAN, a different Bioconductor package may refuse to work with that older version. If you try to install a newer version, you might discover that a different package from CRAN refuses to work with the newer version of the one you've changed. It's all too common to find that a particular package you need will refuse to install for love or money. The process of getting rid of an old version of a package to install a new one can be difficult when you end up installing the same version *again* because of some other version dependency buried in there.

Packages under early development won't have made it into either CRAN or Bioconductor yet, and that you have to download the source code for them. They also tend to be even more fragile when it comes to the versions of other packages they need, by virtue of the fact that they're so new. The silver lining is that R will handle building R packages from source code quite effectively (most of the time).

When we have run R courses as in-person workshops, there has never been a session when someone hasn't had a problem installing a needed package due to these kinds of issues. In fact, when writing *this* course, I discovered that the version of R I was running was no longer supported by Bioconductor *at all*.

You might not run into these sorts of problems. But if you do, fixing them is often a huge time sink. It's probably more sensible to start again from scratch, installing a fresh copy of R, if you can.

Sometimes it's enough to make you want to stare out of the window at some trees and never think about computers again.

### The Tidyverse

The package we installed earlier is a particularly notable one. Because R is quite an old language, it doesn't have many of the niceties that more modern programming languages enjoy. The standard tools for creating plots in R are also a product of their time, and quite finnicky to use.

The [tidyverse](https://www.tidyverse.org/) is a collection of packages with the shared goal of making R (a little) friendlier to use and to make more powerful data manipulation tools available. Going into detail about the tidyverse is beyond the scope of this course, but there are two packages in it of particular note:

- `dplyr` is a package that adds more convenient functions for filtering, aggregating and sorting data objects.
- `ggplot2` is an alternative mechanism for creating plots, known for being both incredibly powerful and also creating publication-quality output.

#### Recap Questions

todo...