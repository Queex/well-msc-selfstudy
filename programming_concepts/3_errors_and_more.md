# Programming Concepts - Errors and More

## Errors

There are many kinds of error that can cause your program to crash. If you write any code, you can expect to encounter them often. Errors are divided into three main types.

### Syntax Errors

These are problems that prevent your code from running at all. You've broken one of the rules of the programming language and the computer cannot work out how to proceed. These are sometimes called **compile-time errors**, because they are identified at compilation. For interpreted languages, compilation is only done when you try to run the code any way, so the distinction can seem small, but syntax errors are errors that, in theory, you could have seen and corrected without needing to run the code.

### Runtime Errors

**Runtime errors** are error that aren't due to incorrect syntax, and only come to light when the code runs. They can still be the product of a mistake when writing the code, for example; trying to load a file with a mistyped name. The code alone doesn't know about what files do or do not exist, so it only finds out about the mistake when it tries to read the file. Other types of runtime error come about due to unexpected input data. Because the code cannot know what input it will receive, these errors can't be automatically detected early. When a program encounters a runtime error, it has to stop immediately.

### Silent Errors

Silent errors are different in that they don't cause your program to crash. Instead, they are errors introduced into the data, that don't cause more serious problems. These are a particularly insidious kind of error because unless you check your program's output against what you know it should produce, you might not even notice them. Silent errors in one part of your code can then go on to cause runtime errors in another part of the code. If you find yourself muttering "where did that zero come from, it should be impossible", you have encountered a silent error.

### Error Messages

Your best tool for fixing an error is the error message you get. Some languages have more useful messages than others. As you get more practice with a particular language, the error messages will become more informative, mostly because you've seen something go similarly wrong before. If you're lucky, the message will include a **line number** to tell you which line of code caused the crash. Of course, if this is a realtime error caused by an earlier silent error, the true problem lies elsewhere.

Another important tool, where the language provides one, is something called a **stack trace**. This is the nested list of the functions that were executing at the time of the error. The last function named is the one where the error took place, and the others are what functions were part way through execution when the error was encountered. Silent errors, again, mean the true error might not be in the most obvious location. 

### Error Handling

It's inconvenient for a program to crash at every little problem. Programming languages provide a way for you to intercept when something goes wrong and fail gracefully in a way that doesn't bring the program to a sudden halt. This is called **error handling**. When you see a message box that says something like "Cannot find file, click OK to continue", that's error handling. It's most useful in situations where there is a lot of user input, and hence a lot of opportunity for user mistakes.

Even in other circumstances, it can be useful for you to handle errors in order to provide more detailed information as to what went wrong. Programming languages have ways for you to create your own errors, which are then handled like any other runtime error, including when it comes to the error message given to a user. A "divide by 0" error is less informative than a "group size must be greater than 0" error. Code that deliberately creates an error, for this reason or others, is said to be **raising** an error.

## Best Practises

It's a common misconception to think that when you write code, you are writing it for the computer. It's true that you are writing *instructions* for the computer, but there are many different ways to write a program that produces the same output. When you are writing code, you are writing code for *whoever needs to look at it in future*. This could be you, months or years down the line, it could be a colleague picking up your project where you left it, or it could be a stranger reviewing your code for accuracy. The over-riding concern, when writing code, is *clarity*. You want to make it as easy as possible to understand what the code is doing and why. 



Programming languages have conventions that fall outside the formal rules of the language. This is often called a language's **style**, and covers things like the preferred way to name variables and functions, how to use capitalisation, how to format the code, and so on. They can also extend to more esoteric programming ideas you probably don't need to worry about.

## 