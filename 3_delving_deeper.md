# The Command Line - Delving Deeper

### Redirection

Many command line tools process text files line by line, meaning they don't need to store the entire file in memory at once. This also means that you can chain them together, making the output of one the input of another. Long chains of commands like this are fairly common when using the command line. Because of this, many commands that handle a file can also take input via something called **standard input**, i.e. the output of the previous command in the chain.

The **pipe** symbol '|' tells the command line to take the output from one command and use it as input for the next.

Here's an example:

`$ ls -a | grep bash | wc`

Let's break down what it does. `ls` shows the files in the working directory (ignore the `-a` for now). This list is then searched for any lines containing the word `bash` using `grep`. Finally, `wc` counts the lines, words and letters in that result.

A common way of working with the command line is to build up these chains of commands piece by piece, seeing what the output is at each stage before deciding what command to add next. This is easier than trying to write it all at once, seeing it doesn't work, and then trying to work out which command went awry.

The other main type of redirection uses the symbol `>`. Instead of sending the output to another command, this puts the output in a file. **This will overwrite any file by that name that existed before.**

`$ ls -a | grep bash > some_files.txt`

will put the list of files found by `ls` and `grep` and write them to a file called `some_files.txt`.

You can now see what the file contains with

`$ cat some_files.txt`

Sometimes you want to add text to a file without replacing what's already there. You can do this using `>>` to redirect to the file.

`$ ls /mnt >> some_files.txt`

You can check that more lines have been added to the file:

`$ cat some_files.txt`

## Arguments and Flags

Some of the earlier examples show commands used with **arguments**. Commands can take a number of arguments after the command itself. The order of these commands is important. The number of arguments, and what they are used for, varies depending on the command – more on how to deal with that later.

Looking at the example for `cp`:

`cp ~/.bashhistory bashhistory2`

The first argument is `~/.bashhistory`, which for `cp` is the file to copy. The second argument is `bashhistory2`, which is the destination.

The command line works out which words are commands and which are arguments by looking for spaces. For this reason, if you need to put a space in an argument, you have to enclose the argument in double quotes. The `echo` example, earlier, shows this in practice:

`$ echo "Look at me"`

There is one argument here, which `echo` will interpret as `Look at me`, without the quotes.

Commands also use **flags** (also known as **options**). A flag is an instruction to the command to behave in a certain way, or to expect certain arguments. Flags are usually single characters, preceded by a `-`. Because they are single characters, you can also put them together after a single `-`.

`$ ls -alh`

For `ls`, the flag `-a` says to show *all* files. The convention for making files hidden in UNIX is to make the file name start with `.`. `ls`, by default won't show you these files (which includes `.`, the directory itself, and `..`, the directory one level up).

The flag `-l` says to present the output as a list (i.e. a table), with columns containing extra information about the file. This includes the date the file was last modified, and the size of the file. The flag '-h' modifies the list so that the file sizes are made 'human readable', rather than listed in bytes.

Although this is a very terse and efficient system, it relies on you memorising (or looking up) which flag you need to set. Many commands have longer versions of these flags, with `--` before them, which helps make the line more readable. For example:

`$ ls --all`

Is the same as 

`$ ls -a`

When you use these longer flags, they need to be separated. So the equivalent of the earlier example is:

`$ ls --all -l --human-readable`

In this case there's no long version equivalent of `-l`.

Some flags themselves require arguments, which can be specified in one of a number of different ways:

`$ ls --time=ctime`

`$ samtools sort -T /tmp/aln.sorted -o aln.sorted.bam aln.bam`

In the first example, the long flag `--time` requires an argument, given after the `=`. In the second example, the `-T` and the `-o` are specifying what the following arguments are to be used for. This second approach avoids having to give arguments in a set order. If these different approaches seem annoyingly inconsistent, it's because they are. The approach used was at the whim of whoever wrote the command.

### Getting help

The best resource for finding out how to use a command is a web search: the command name together with 'bash' is most likely to find something useful. The command line has its own methods of showing help, but they are designed to be viewed in the terminal and it's more convenient to have them in a different window.

Some commands will provide more information if you use the `--help` or `-h` flag. Almost all commands have something called a 'man page' (short for manual) that goes into detail how to use the command.

For example:

`$ man ls`

You can scroll through the help with arrow keys, and quit back to the command line proper with 'q'. The one advantage this method has over a web search is that you are guaranteed to get correct information for the precise version of the command you have on your system, for occasions where command line tools have different versions.

What none of these methods do very well is help you find commands you don't know about, but which would be useful for the task you're trying to do. A web search for your problem is your best bet, if you're trying to do something but you don't know where to start.

Here is a list of other commonly-used commands you might find useful. You can look up the details on how to use them using `man` or a search engine.

| Command | What it does |
| --- | --- |
| `head` | Shows the first few lines of a file. |
| `tail` | Shows the last few lines of a file. You can combine `head` and `tail` using pipes to pull out a specific block of lines from a file. |
| `touch` | Changes the accessed and modified time on a file, by default to the current time. If the file doesn't exist, create a blank file. |
| `which` | Tells you the absolute path of the command you give as an argument. This is useful when there might be multiple versions of the same command available on the system and you need to know exactly which one is used by default. |
| `sort` | Sorts the lines of a file. |
| `uniq` | Prints unique lines in a file (i.e. removing duplicates). It does not work exactly as you might expect, only removing duplicates on sequential lines. To get the truly unique output, you need to use `sort` first. |
| `wget` | Short for 'web get', this tool downloads a file from the internet, by default into the current directory. Note that on some systems, most notably computing clusters, the computer you are using might not have an outside internet connection. |
| `ssh` | Short for 'secure shell', this logs you into a different computer, based on the address you give it. |
| `scp` | Short for 'secure copy', this allows you to copy files between different computers, providing you have a valid log in for the other computer. There are a number of other protocols for transferring files, but some have fallen into disuse and `scp` is the most widely supported. |
| `gzip` / `gunzip` | Turns a file into a compressed version of itself (with the `.gz` file extension), or turns a compressed file back into a regular one. Unlike the compression tools you might be used to, this only works on single files, and you cannot put multiple files or directories into a single compressed file using `gzip` alone. **By default, it will delete the input file after compressing or decompressing it.** |
| `tar` | This takes a number of files and puts them all into the same file (sometimes called an archive - the command is actually named as an abbreviation of 'tape archive'). `tar` can also handle `.gz` compression itself, with the `-z` flag, making `gzip` somewhat redundant.. It's common to see files for download with the combined extension `.tar.gz`. Unlike `gzip`, you use the same command to get the files back out again, just with a different flag, and `tar` does not delete the input file(s). `tar` also does not behave nicely if you don't specify the output file using the flag `-f`. At this point, you might have some inkling as to how programmers got that way, if this is what they have to deal with. |
| `cut` | Print certain columns from a text file that's a table of data. |
| `awk` | Can do similar things to `cut`. It has its own language to specify in more detail how to process the file, which can be tough to learn, but it is more versatile than `cut`. |
| `tr` | Short for 'translate'. It lets you replace characters with other characters. This is useful to fix inconsistent data formats or remove characters that another tool can't handle. |
| `sed` | Short for 'stream editor'. Similar to `tr`, but it also supports more than single characters allowing for more complex replacements. |

### Globbing

Sometimes you want to refer to a number of files without having to type their full names. UNIX shells offer a feature called **globbing** (no, really) to help with this. It uses special characters that the operating system will expand into *every* matching file.

The most often used globbing symbol is `*`. This means 'any number of characters in the filename, or even none'. 

For example:

`$ cp myfile*.txt another_directory/`

This will look for every file in the working directory that starts with 'myfile' and ends with '.txt', no matter how many of them there might be. It would match any of the following files, if they existed:

- myfile1.txt
- myfile2.txt
- myfile169.txt
- myfile_and_only_my_file_so_hands_off.txt
- myfile.txt
  
It would not match any of the following:

- this_is_myfile.txt
- myfil.txt
- myfile.txt.gz
  
Command line tools know how to treat these groups of files sensibly. In the above example, all matching files will be copied into the directory `another_directory`.

You can even use the `*` all by itself, to match every file. For example, if you wanted to remove all the files in a particular directory:

`$ rm some_directory/*`

has got you covered. You can use it to match directories as well as files:

`$ rm directory_number_*/unwanted_file.log`

will remove the file with the same name from all those folders at once. You can even combine those two ideas:

`$ rm */unwanted_file.log`

Be aware that because `rm` does not ask for confirmation when it removes files, using it with `*` can be *very* dangerous. Not in terms of damaging the operating system, because that's protected (or at least it should be), but because you might accidentally delete a lot of files you really, really wanted to keep.

`*` is called a 'wildcard', and this approach to handling multiple files has spread far and wide because it is so useful. There are other wildcards available, but `*` is the most important.

#### Recap Questions
Let's try a short practical task, using the commands we've covered.
1. Download the file: [https://www.well.ox.ac.uk/bioinformatics/training/MSc_GM_2022/CM4-2-command_line/data/dna.txt](https://www.well.ox.ac.uk/bioinformatics/training/MSc_GM_2022/CM4-2-command_line/data/dna.txt) using `wget`.
2. Find how many lines contains the *DNA motif*  `CGAT` somewhere on that line.
3. Find the line numbers for those lines.
4. To find the *reverse complement* of DNA sequence, you have to swap all Cs and Gs, and all As and Ts, and print the sequence backwards. Can you print the reverse complements of the lines in the above file? Looking up the help for the `rev` command will be useful.
5. How many lines in the reverse complement contain the motif `CGAT`?

The last couple of questions are actually quite tricky, so don't get disheartened if you can't work them out!
