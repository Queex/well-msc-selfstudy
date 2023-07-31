# Answers to the recap questions:

## Introduction

1. The most common UNIX-style shell is: 2. bash
2. You can only use the UNIX-style command line on Linux computers: 2. False
3. Compared to using a graphical user interface, the command line is: 3. sometimes faster
4. What is best practice when using the command line: 4. Keep a record of the commands you have used
5. The built-in option for a UNIX-like command line on Windows is: 1. WSL

## The Basics

1. Use *Control+c* to cancel the current command and return to the prompt.
2. The `~` symbol is the shorthand for your home directory.
3. `../../../` refers to the directory **3** levels up from the current one.
4. You probably instinctively tried to use *Control+c* to copy, instead of *Control+Shift+C*. You cancelled the (blank) current command and went back to the prompt.
5. You can use `cp` to copy the file, then `rm` to remove the original file.

## Delving Deeper

1. The command `$ wget https://www.well.ox.ac.uk/bioinformatics/training/MSc_GM_2022/CM4-2-command_line/data/dna.txt` will download the file into your current directory.
2. Hint: look at the commands `grep` and `wc`.
   1. The command `$ grep CGAT dna.txt | wc -l` will find the lines using `grep`, and `wc` with the `-l` flag only reports the number of lines.
   2. You can accomplish the same just using `grep`: `$ grep --count CGAT dna.txt` or `$ grep -c CGAT dna.txt`.
3. Hint: the same commands as above are the place to start, but maybe explore what flags they have available.
   1. The command `$ grep -n CGAT dna.txt` will print the line numbers alongside the lines.
   2. You can make the output prettier by also using `cut`: `$ grep -n CGAT dna.txt | cut -f 1`
4. Hint: the best command to use for the character replacement is `tr`.
   1. The command `$ cat dna.txt | tr CGAT GCTA | rev` will reverse complement the lines.
   2. Note that the `tr` command does not have an argument where you can specify a file, you have to use `cat` to print the file and pipe that into `tr`.
   3. You can do the same task with `sed`, but it is somewhat messier because `tr` does all the substitutions at once, whereas with `sed` you have to do them sequentially.
      1. `$ cat dna.txt | sed 's/C/x/g' | sed 's/G/C/g' | sed 's/x/G/g' | sed 's/A/x/g' | sed 's/T/A/g' | sed 's/x/T/g' | rev`
      2. The `s` is an instruction to sed to *substitute* characters.
      3. The `g` tells sed to do this substitution for every occurence of that character on a line, not just the first.
      4. We use the dummy character `x` to do each swap in three substitutions.
      5. `tr` is clearly the better options here, if only because there is less scope for error!
5. Hint: you can either pipe your previous result straight into `grep`, or redirect it to its own file.
   1. The first way: `$ cat dna.txt | tr CGAT GCTA | rev | grep -c CGAT`.
   2. The second way: `$ cat dna.txt | tr CGAT GCTA | rev > dna2.txt`, then `grep -c CGAT dna2.txt`.

## Appendix

1. The likeliest problem is that you forgot to specify a file early on in the chain, and one of the commands that was expecting input from that file is instead waiting for other input. Using `Control+c` should break out of the command and return you to the prompt.
2. If **standard input** is what some commands can accept from `|`, it makes sense that **standard output** is the equivalent for the output of a command; what you usually see printed on the command line. **standard error** would, presumably, be something similar, but just for messages about errors. This is, in fact, the case! Although the command line will print both **standard output** and **standard error** to the terminal window. Sometimes, they can even tussle, and you get the text from both interspersed, line by line!
3. It's sensible to assume that they show the start or end of a file or piece of data repsectively, although the specifics might require you to study the help for them to use them properly.
4. Some variation on `$ grep -lv error * | tar -czf non_errors` will get the job done.
   1. This uses `grep` with globbing (`*`), searching every file in the current directory.
   2. The `-l` flag says to report the filename for any files where there is a match, and the `-v` flag says to invert matching, so only files *without* that text will be reported.
   3. `tar` has the flags `-c` to create the archive, `-z` to use `gzip` on the archive and `-f` to specify the file name for the archive, which will get the relevant sufffixes applied to create the file `non_errors.tar.gz`.

   