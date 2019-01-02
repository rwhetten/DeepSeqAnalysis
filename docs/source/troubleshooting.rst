.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Troubleshooting
===============

General advice on troubleshooting
*********************************

This page provides tips and advice for what to do when things go wrong in the Linux command-line environment. Everyone makes mistakes; the difference between experienced users and inexperienced users is how long it takes to understand what the mistake was and fix it.

"The computer does what you tell it to do, not what you want it to do."

Make sure you are telling it to do what you want it to do: RTFM

**man command** will give documentation for standard Linux utilities and some installed packages.

**tldr command** gives briefer and more user-friendly examples of how to use common commands (if the tldr package is installed)

Types of problems
*****************

Some examples of common types of errors.

1.	**Nonexistent command or file path** If the computer doesn't understand what you are telling it to do, it will return an error of "no such file or directory" or "command not found". This can be as simple as a spelling error in the command, but other common causes are failing to give the full path to the software you are trying to run, or failing to give the full path to the file you want it to use. Try using 'pwd' to see where you are in the directory tree, and 'ls' to see what files are in that directory. If the file you want to use is not in your current working directory, you will have to give either a relative path or an absolute path to the file when you issue your command. If you are trying to use a software tool that is in a location that is not on the search path, try giving the absolute path to the executable file followed by the -h option - often this will print the software version and help screen to let you know the program was found. To find out which directories are on the search path, type **echo $PATH** at a terminal prompt.

2.	**Incorrect use of a command or incorrect file format of an input file** This type of error often leads either to a cryptic error message, or perhaps no error message is returned but nothing happens either. This can happen if you don't read the documentation well enough, or if the documentation you carefully studied applies to a different version of the software than the version you are trying to run. Reading documentation online while trying to use software installed on a local machine makes this an easy mistake to make. Online resources may be more recent than the locally-installed version of the software, and describe functions that aren't available in the version you are trying to use. Alternatively, the online resource you found may be out-of-date (even though it is only 6 months old) and no longer applies to the version of the software installed on your machine.

3.	**Incorrect use of a command, so that the program runs but does something different than intended** This is the most dangerous kind of mistake, because it can be very difficult to recognize. This is one of several reasons why it is a good idea to test out commands individually before linking them together into a pipeline, and use a small but diverse trial dataset for those initial tests so that unexpected results can be spotted relatively easily.

4.	**An empty or smaller-than-expected output file is produced by a loop** If you use a bash loop to run a command that (by default or optionally) creates a new file to write output to, remember to change the output filename each cycle of the loop to avoid overwriting earlier output files with the most recent one. If you want all output written to the same file, it may be best to direct output of each command to STDOUT (the screen), then redirect output from running the loop to a single file. Alternatively, redirect output from each execution of the command to a file using >> (to append) rather than > (to overwrite).



Keys to troubleshooting
***********************

1.	Confirm that file paths and command names are spelled correctly - typing errors are probably the most frequent problem. Make sure you use enough information to allow the computer to find the command you want to use and the files you want to process with that command.

2.	Confirm that the tool you are trying to use is the right one for the task you are trying to do. There are usually many different ways to do a particular task in Linux, but there are infinitely many more wrong ways than right ways.

3.	Find the documentation for the program you want to use, and make sure the version of the documentation matches the version of the program you are using.

4.	If you are troubleshooting a loop, manually write out the values of variables used and names of files written in each cycle for the first two or three cycles. If you are using nested loops, do this for the first two or three cycles of each of the nested levels, to confirm that the variable values are being updated as you intend and output is written to uniquely-named files to prevent overwriting data.


Last modified 2 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
