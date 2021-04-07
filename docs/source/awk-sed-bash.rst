.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Awk, Sed, and Bash: Command-line file Editing and Processing
============================================================



Global Overview
***************

The process of collecting, managing, and analyzing high-throughput sequencing data requires the ability to handle large text files, sometimes 10 Gb or more in size. Command-line tools optimized for efficiency and speed are often the best for simple tasks of summarizing data, modifying file formats, and automating repetitive tasks. The four steps of computational thinking are directly applicable in this context - break a complex problem down into simple steps, look for patterns and similarities among steps, then find a general solution for each class of steps and put those solutions together into an algorithm or pipeline that will accomplish the desired task. For repetitive tasks, loops are a useful tool that allow a script to carry out the same sequence of commands over and over until a desired endpoint is reached.


Objective
*********

Awk, sed, and bash are command-line tools that provide tremendous power for managing and manipulating text files of arbitrary size, from very small to extremely large. The objective of this class session is to give course participants experience in using these tools to carry out specific tasks, and experience in searching on-line resources to find out how to accomplish specific objectives with these tools. 



Description
***********

The `bash shell <http://cs.lmu.edu/~ray/notes/bash/>`_ is the default command-line user interface in the Lubuntu 18.04 Linux system used for the course. A shell script is simply a text file that contains a series of commands recognized by the bash shell, which allows users to create standard workflows and use them over and over with different input files. This is a powerful tool to automate routine or repetitive tasks in data management or analysis, and learning some basic skills can make these tasks much easier. `Awk <http://tldp.org/LDP/abs/html/awk.html>`_ is a scripting language that is particularly well-suited to handling tabular data in text files, such as SAM alignment files or VCF files of DNA sequence variant data. `Sed <http://tldp.org/LDP/abs/html/x23170.html>`_ is a "stream editor", a program that allows manipulation of text files one or two lines at a time, as the text passes through a series of piped commands. The capabilities of these three tools overlap, and many tasks can be accomplished using any of them, but each has its own particular advantages for specific types of problems. Handling multiple files is made easier using file globbing, as described in the `FileGlobbing.pdf <https://drive.google.com/open?id=1nvy5IynatYLkztRcRGomkWZkFEbwxS9b>`_ document, while the `RegularExpressions.pdf <https://drive.google.com/open?id=1m3OR0Wx5NAj6rbZ9F6dg3gSc56djIVL0>`_ file has provides an overview of regular expressions, a more general and powerful tool for pattern matching in text files. A powerpoint presentation from a previous year's lecture is available `with this link <https://drive.google.com/open?id=1csbwJ8Dc4j4VeTw2TT8aihHMe2aZJwe0>`_.




Key Facts
*********

Sequence data analysis often requires the ability to examine and modify the contents of text files, and this is exactly the purpose for which awk and sed were designed. Combining these tools with command-line utilities such as cut, sort, uniq, grep, and other shell functions provides powerful capabilities for summarizing or re-formatting data files. The "modulo" operator (%) in awk, for example, is well-suited to the challenge of working with sequence files in FASTA or FASTQ format, where specific information is found in a particular line within each group of two (for FASTA) or four (for FASTQ) lines. The `bioawk <https://github.com/lh3>`_ version of awk removes the need for this trick by allowing the user to specify that the input file format is 'fastx', meaning either FASTA or FASTQ, and the program then assigns the variables $name, $seq, and $quality to the appropriate records in the input file. Another specialized version of awk is `vawk <https://github.com/cc2qe/vawk>`_, which is designed for manipulation of VCF files containing data on the locations of SNPs and other sequence variants as well as which alleles of those variants are detected in a set of samples. Both of these programs are installed in the VCL machine image, so you can compare them and decide for yourself which you prefer. A sample VCF file is available `here <https://drive.google.com/open?id=1AwQK8LaUvFJwbl4UEvxfLYOpzuWMnNud>`_ for use with bioawk and vawk; the official `format specification <https://vcftools.github.io/specs.html>`_ for the Variant Call Format is available on the Github website for `VCFtools <https://vcftools.github.io/index.html>`_.



Exercises
*********

`awk_sed_bash.txt <https://drive.google.com/open?id=1hJQ0D844YDBrZz6XUhP3JsXyT-iE2vLS>`_ has the list of links for the data files needed for the following exercises.



1.	`Bash and awk exercises <https://drive.google.com/open?id=1C0xepbOtdDy2d3yN-VmNUyQ71903XBCY>`_. Writing and executing loops is a key skill to learn in programming, because this makes completion of repetitive tasks much easier. The bash shell also provides a wide variety of tools to manage system functions, maintain software, and track system resources. Awk allows use of both conditional statements and loops to process and manipulate text files, and can carry out many text-processing activities commonly done using spreadsheet programs in a Windows environment. Awk can do basic arithmetic, but is not intended for statistical analysis - datamash is a better option for doing basic statistical summaries on large tabular files.

\

2.	`Exercises <https://drive.google.com/open?id=1yxRhkbvPuzVe6Nx_DURLK-Dxr-UZPuhN>`_ using find, sed, bioawk, and bash to find and modify files.

\

3.	Handy tips for `bash <https://drive.google.com/open?id=14fm1hndRXcoXtuSQPD94bZrkP9HSXVKJ>`_, `awk <https://drive.google.com/open?id=1erhO5seRwopHXMDNPDbbQvehknuioMOo>`_ and `sed <https://drive.google.com/open?id=1onizOqB0JaUHZyhXEezmGUg0M3L6neDa>`_ - these are examples I have saved from my own applications of these tools. You may find some of these tips useful, but these lists are by no means complete, so feel free to add additional information and keep your own list of the most useful tricks for each of these tools.

\

4.	An online resource called `Linux Command Line Exercises for NGS Data Processing <http://userweb.eng.gla.ac.uk/umer.ijaz/bioinformatics/linux.html>`_ is mostly about awk.

\

5.	One feature of the bash shell mentioned in the list of handy bash shell tricks is `parameter expansion <http://mywiki.wooledge.org/BashGuide/Parameters#Parameter_Expansion>`_, which offers a range of tools for modifying the values of variables. One example of the utility of these tools is processing a set of FASTQ sequence files - suppose there are samples named S001 to S150, so the sequencing center splits the reads into 150 files named S001.fq.gz to S150.fq.gz. If all these files are saved in a directory, a bash loop can be used to align them to a reference genome, but simply using the input filename as the base for the output alignment file will result in files named S001.fq.gz.bam to S150.fq.gz.bam, in which the "fq.gz" no longer serves a meaningful role. For a variable called $file, parameter expansions such as ${file%%.*} can be used to retrieve specific parts of the string of filenames and extensions. The ${file#} and ${file##} constructs remove matched patterns from the left end of the string stored in the $file variable, while the ${file%} and ${file%%} contructs remove matched patterns from the right end of the stored string. `Examples <http://wiki.bash-hackers.org/syntax/pe>`_ make this somewhat more clear, but the best way to see how it works is to practice (for example on the files saved in the `AtRNAseq <https://drive.google.com/open?id=1_-cX7Scvp_e8zlN4glcD3-i2eJg5Tv71>`_ archive).

\

6.	Another useful tool in bash is `process substitution <http://tldp.org/LDP/abs/html/process-sub.html>`_, the ability to nest commands inside other commands to combine outputs from different files and commands into a single process.  For example, to compare column 2 from one multi-column tabular file to column 3 from a different tabular file and report differences between them: 

::


	diff <(cut -f2 file1) <(cut -f3 file2)


\

7.	`Basic walkthrough of AWK <https://drive.google.com/open?id=1xuWyJCFegjVfxNw5iz9PvecVliDdqjOZ>`_ from chapter 1 of "The AWK Programing Language" with datamash examples as well. A scan of the complete text of  `The AWK Programing Language <https://drive.google.com/open?id=1B9gz-XLbQBDkxIQdbJVCzWgy2H3UNlIP>`_, is also available - this is the authoritative resource for AWK, written by the original authors of the language.

\

8.	`Datamash examples and exercises <https://drive.google.com/open?id=1xMsvOyZI18WJgikMbhGiMwvBDb2x35Rs>`_ is a text file with example problems for practice with Datamash as well as a comment on how to deal with non-uniform filenames. 

Additional Resources
********************

+	A `Bash Guide for Beginners <http://www.tldp.org/LDP/Bash-Beginners-Guide/html/>`_, an `Introduction to Bash Programming <http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html>`_, and the `Advanced Bash-scripting Guide <http://www.tldp.org/LDP/abs/html/>`_ are all available on The Linux Documentation Project webpages. The Advanced Bash-scripting Guide also includes appendices with introductory information on `awk <http://tldp.org/LDP/abs/html/awk.html>`_ and `sed <http://tldp.org/LDP/abs/html/x23006.html>`_.

\

+	The GNU `awk manual <https://www.gnu.org/software/gawk/manual/gawk.html#Getting-Started>`_ and `sed manual <https://www.gnu.org/software/sed/manual/sed.html>`_ are available on the `www.gnu.org <www.gnu.org>`_ website.

\

+	The site `www.panix.com <http://www.panix.com>`_ has information on several aspects of the Unix or Linux command-line interface: `sed <http://www.panix.com/~elflord/unix/sed.html>`_, `grep <http://www.panix.com/~elflord/unix/grep.html>`_, and `bash scripting <http://www.panix.com/~elflord/unix/bash-tute.html>`_.

\

+	`Datamash main page <https://www.gnu.org/software/datamash/>`_ with links to helpful examples and one-liners. A html `Datamash manual <https://www.gnu.org/software/datamash/manual/datamash.html>`_ is also available. 

\

+	Bruce Barnett's Unix tutorials page at `grymoire.com <http://www.grymoire.com/Unix/>`_ includes tutorials on `awk <http://www.grymoire.com/Unix/Awk.html>`_, `sed <http://www.grymoire.com/Unix/Sed.html>`_, `grep <http://www.grymoire.com/Unix/Grep.html>`_, and `regular expressions <http://www.grymoire.com/Unix/Regular.html>`_, and links to Unix and Linux-related books.

\

+	The IBM developerWorks site has a three-part series on `awk <https://www.ibm.com/developerworks/library/l-awk1/>`_.

\

+	The blog `TheUnixSchool <http://www.theunixschool.com/>`_ has a page with example `awk and sed <http://www.theunixschool.com/p/awk-sed.html>`_ commands to accomplish specific tasks, as well as a grep search function to find previous postings on any topic of interest (look on the right side of the page, below the "join us on RSS Twitter Facebook Google+" box).

\

+	The LinuxCommand.org website contains tutorials called `Learning the Shell <http://www.linuxcommand.org/lc3_learning_the_shell.php>`_ and `Writing Shell Scripts <http://www.linuxcommand.org/lc3_writing_shell_scripts.php>`_ that provide a good introduction to shell commands and strategies for writing scripts to combine individual commands into a coherent and efficient workflow. There is also a link to a book called `The Linux Command Line <http://www.linuxcommand.org/tlcl.php>`_ which can be downloaded as a PDF.

\

+	`A quick guide to organizing computational biology projects <http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424>`_. Noble, PLoS Computational Biology 5:1000425, 2009 *This paper offers a suggested organizational plan for keeping track of data from different experiments and projects in a structured set of directories and files. It is focused on bioinformatics students, so it emphasizes source code and programs more than experimental data or field notes, but the general strategy is applicable to many disciplines.*



Last modified 7 April 2021.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
