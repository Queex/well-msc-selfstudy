# Programming Concepts - Introduction

Learning a programming language from scratch can seem daunting. A really effective way to break through that barrier is to start writing code as soon as possible, altering existing code and seeing what changes, tinkering until you get you want.

Sometimes, though, what's going on in the code can be just a little too complicated, or a little too obscure, for it to be easy to tell *what* you need to change. The purpose of different bits of code can be unclear, and changing one small thing can stop the code from working in a way you don't understand. It's also possible, even when you *succeed* at altering code, to misunderstand what's happening behind the scenes and then trip over that misunderstanding when you come to code something else. Finally, it can be easy to think that *all* programming languages behave the same way as the one you have started using, and get into a pickle that way.

There's no way to *prevent* such misunderstandings completely. This course is designed to teach a handful of extremely general ideas about programming, not specific to any particular language, that should help avoid falling into those traps later. It's informational, not assessed, and entirely optional.

## Compiled Versus Interpreted

Traditional programming languages are **compiled** languages. After writing your code, you run a tool called a *compiler* that turns your code into a binary file you can run. If you've made a syntax error, then the compiler will spit out an error instead of compiling your code. However, just because your code compiles, that does not mean it's doing what you want it to! Many coding errors won't stop the program from running, but will make it do the wrong thing or produce an incorrect answer. Modern programmers usually use something called an *Integrated Development Environment*, or *IDE*, that lets you compile and run your code at the touch of a button. Most of them will also check your code for syntax errors in the background while you are typing, giving you instant feedback similar to a spell-checker. However, even when using one of these tools, the compilation still needs to happen somewhere. Compilation is also specific to your operating system, so it is necessary to compile your program separately for each platform you intend to run it on.

*Examples of compiled languages: C++, Go, Haskell*

The main other type of language is an **interpreted** language. In these languages, you do not expressly compile your code, but instead run it directly. Technically, what happens is that your code is run through an *interpreter*, which compiles your code in the background just before it runs. This makes it simpler to run your code, but you will only discover errors when you try to run it, as there is no explicit compilation step. IDEs will also check interpreted code as you type it. Interpreted code is more *portable* than compiled code, in that you don't need to prepare separate versions for different operating systems, only share the file containing the code you have written. Files containing interpreted code are often called *scripts*. Strictly speaking, interpreted code is slower than compiled code (because for the former, the compilation happens as you run it), but there are very few situations where that makes any discernable difference with modern computers.

*Examples of interpreted languages: MATLAB, Python, R*

## Comments

Code, by itself, can be annoyingly opaque. **Comments** let you leave plain text messages in your code to explain what it does. You will not see these comments when you run your code; they are there to make it easy to understand the code itself when you or someone else reads it. Comments should not merely restate what the code does, but explain *why* the code is doing that and *how* is does it, if the latter is not obvious.

Comments often seem unnecessary until the first time you need to alter some code you wrote six months ago and you realise you no longer remember a single thing about it.

## Libraries

A **library** is a collection of pre-written code (generally in the form of 'functions', which will be explained later) you can use when writing your own code. They are, primarily, an *organisational* convenience to help make writing code cleaner and simpler. Even if you programming language has a wealth of features and functions available, only the most essential functions will usually be available by default.

To use the other features, you need to put something in your code to say you want to use one of these additional libraries. The specifics vary by language, but you generally say you will **import** a package or library. Once you have put a line in your code to do this, you have access to all of its functions in the rest of the code.

Apart from the libraries that are considered a part of the programming language, there are also **third-party libraries** available. Before you can import one of these packages, you will likely need to install it into your development environment. The precise way you do this is highly dependent on the programming language, but the key point is that third-party libraries are not *always* available, unlike the standard (i.e. first-party) libraries that are a part of the programming language.

