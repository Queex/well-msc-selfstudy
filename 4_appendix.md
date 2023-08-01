# The Command Line - Appendix

### Command Line 'Applications'

Because of its origins as an operating system, there are many command line tools that behave like windowing applications, such as text editors and various kinds of viewers. The limitations of command line graphics mean they can only show text, they (usually) take up the entire terminal screen, and you can only control them using the keyboard.

The `man` command, mentioned earlier, is one such application. Or rather, `man` looks up the correct help pages and sends them to another tool called `info`, which displays them (an example of redirection in practice).

These different applications tend not to be consistent with what keys do, although in most of them `q` will quit and put you back on the regular command line. If you find yourself in such an application and can't work out how to get out of it, in most cases `Control+c` will probably get you home.

Some useful command line applications are:

- `top` will show a table of what processes are running on the computer, similar to Task Manager in Windows. Press `q` to quit.
- `more` allows you to read a text file. It's more convenient than `cat` because you can scroll back and forth through the file. It's also common to use `|` to redirect text output into `more` to look through it more easily. Press `q` to quit.
- `less` performs the same task as `more`, but behaves slightly differently. It's a matter of personal taste which people prefer to use. The name is more programmer humour. Press `q` to quit.
- `nano` is a text editor. If you are used to graphical user interfaces, not being able to position the cursor with the mouse might take some getting used to. Press `Control+x` to quit.

### Scripts

Because use of the command line is a sequence of instructions, it's possible to put the sequence into a text file, and tell the command line to run all the commands in the file, one by one. This is called a **script** or **shell script**, and the convention is to give these scripts the `.sh` suffix (for 'shell').

Scripting for the command line is a programming language in its own right, way outside the scope of this course. Scripts offer some features to control the behaviour of the command line that would be redundant when typing commands directly, and complex scripts can be hundreds of lines of terse code. It's good practice to make liberal use of comments (using `#`) to describe what your scripts do. This is particularly the case for future you, looking at the script months or years after you wrote it.

For your purposes today, it's enough to know that scripts exist. If you ever need to run a script someone else has made, you do so as you would run a command:

`$ ./some_script.sh`

You need the `./` at the front to tell the command line that you want to run that specific script, rather than have it search for a command by that name in its internal libraries.

UNIX and its derivatives have a permission system that controls who can read and write files and who can view directories and run commands. You might find, when running a script, that you receive an error similar to:

`permission denied error.`

This means that the script has not been set up to allow you to run it. The simplest way of fixing this is by using the command:

`$ chmod u+x ./some_script.sh`

You don't need to sweat the details as to how this works, as a description of the permissions system is also beyond the scope of this course.

#### Queues

Most computing clusters have a system where rather than running your commands directly, you have to put them into a script and then submit that script to some kind of queueing manager. This program will keep your script waiting until the cluster has the resources to run it.

### Bioinformatics Tools

As mentioned, many tools used in bioinformatics run from the command line. Most are used to process a specific kind of data file into another data file. Because these files are often very large, they work with compressed file formats. Even when compressed, these files can be very large. It's often necessary to store different versions of the data (e.g. raw and processed files) and the storage requirements can rack up quickly.

Although some of these tools follow the usual paradigm of processing the files line by line, the most computationally-intensive tools need to store a lot more in memory, resulting in very large memory requirements that are often beyond that available in a desktop computer. For these tools, access to a computing cluster, cloud computing solutions, or a suitably powerful server is required.

When working with bioinformatics tools, it's important to be mindful of storage and memory requirements – you don't want to be embarrassed by having nowhere to keep your data once it's been processed!

The computing side of bioinformatics merits its own course, but as a brief overview of some of the tools:

- **BEDtools** manipulates lists of genomic regions; looking for overlaps, intersections and so on.
- **BLAST** compares sequences to genomes references.
- **featureCounts** collates which features are observed in an aligned data set, and how frequently they appear.
- **GATK** (Genome Analysis ToolKit) performs many tasks, including alignment.
- **Picard** provides quality control and other metrics for genome data.
- **Salmon** is another alignment tool.
- **SAMtools** manipulates files containing mapped sequences, providing summaries and output in a variety of formats.
- **STAR** is yet another alignment tool.
  
This is far from a comprehensive list; and does not include visual tools, even when they are run from the command line. It does not matter if you are unsure how these fit together, or what 'alignment' is , at this stage. The world of bioinformatic software is wide and complicated and it's best to explore specific tools when you have a definite need to use them.


### Other Command Lines

Apart from bash and its analogues, command lines can be found in many other places. Even modern releases of Windows have a version of the old MS-DOS command line. However, every command line is its own beast, with its own quirks. It's common to have some commands named the same as the equivalent commands in other systems, but it's not guaranteed.

Many programming languages also have a command line where you can enter lines of code directly. This is very useful to test out code to make sure it does what it's supposed to before including it in your program.

For example, the **python** programming language comes with a command line called 'IDLE', and it uses the prompt `>>>`. The **R** statistical language runs as its own command line, and uses the prompt `>`.

Both of these are command line applications you can start from the bash command line. Each of them having a slightly different prompt is a useful aid to knowing which sort of command line you are typing into.

### Wrapping Up

There's a lot to get to grips with in this course. It's worth bearing in mind that no-one, no matter how practiced with the command line, types perfect commands every time. The process of using the command line is always experimentation, tweaking things until you get the correct result. It's common when starting out to make mistakes, and lots of them, and to end up with commands you've written where you don't fully understand how or why they work. Don't get disheartened by this. Sometimes all you need is another pair of eyes on the problem to see what's wrong, or for someone to tell you about a useful command you hadn't encountered before then.

#### Questions to Think About

Remember you can look at the help files for commands to find tweaks to how they behave.

1. You are writing quite a complicated series of commands joined by `|` symbols. When you run it, instead of seeing output, you are left with blank lines you can type into. What do you think might have gone wrong? How might you return to the prompt?
2. From context, what do you think **standard output** and **standard error* might refer to with respect to the command line?
3. If you encountered the functions `head` and `tail` in a different programming language, what would you assume they did?
4. If you had a large folder of text files, and you wanted to compress them into a single compressed file, but only if those files didn't contain the word 'error', how might you approach it?
5. Why do you think the `uniq` command only removes duplicates in consecutive lines?

Model answers to these, and the recap questions, are given in the next section.
