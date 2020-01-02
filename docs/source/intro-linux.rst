.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Introduction to Linux and the Command-line Interface
====================================================

Objective
*********

The objective of these class sessions is to introduce participants to the Linux computing environment, with a particular focus on the Unix environment provided as a virtual machine through the NC State `Virtual Computing Laboratory <https://vcl.ncsu.edu/>`_. An introductory lecture on key elements of Linux system architecture and computing philosophy will be followed by hands-on computing exercises to provide experience in using command-line utilities to navigate the file system, manage files and directories, and carry out basic file processing tasks. Demonstrations of how these command-line utilities can be applied to sequence analysis tasks are integrated into the exercises.


Description
***********

Introductory `slides provide <https://drive.google.com/open?id=14abKXvZShl4DuNfkGX0-dVTYHkKo67-C>`_ an introduction to the course objectives and the Linux operating system in the first class session, and a `summary <https://drive.google.com/open?id=1ztskWkrVwFT0PogGDFw54L6-lppFwpsd>`_ of Chapter 1 from Eric Raymond’s book The Art of Unix Programming  (complete text available `here <http://www.catb.org/esr/writings/taoup/html/>`_) is used as a framework for discussion of differences between the Linux command-line interface and graphical interfaces. File globbing and regular expressions provide a basis for discussion of abstraction and generalization as key parts of computational thinking. 


Global Overview
***************

Linux is the operating system of choice for computationally-intensive data analysis, because of its design and the efficiency with which it runs. Much open-source software for sequence data analysis is written for Linux, although there are an increasing number of Java-based programs that can run under Windows. A key element of the philosophy behind Unix and Linux operating systems is decomposition of tasks into simple categories – separate command-line utilities are available for separate tasks. Combining these simple individual tools into pipelines provides enormous flexibility for managing and processing data. Abstraction is another key concept in computing - generalizing from a specific case to a larger group of cases that all meet a specific set of criteria. The use of "wildcard" or meta-characters to specify groups of files is a simple example; this process is commonly called file globbing. Regular expressions are another powerful example of  abstraction and generalization as key parts of computational thinking.


Key Facts
*********

DNA sequence data and most results of analysis are stored in plain text format, often compressed using an open-source algorithm to reduce the size of the files stored on disk. A few dozen commands for manipulation of text files, executed either separately or in different combinations, provide an  enormous range of data manipulation and analysis capabilities. A modest investment of time in learning basic file formats and commands for text file manipulation will pay large returns by enabling you to manage large data files and carry out basic analyses on the command line, without any specialized software for sequence analysis.


Exercises
*********

1. An `Introduction to Linux and Lubuntu 16.04 <https://drive.google.com/open?id=1-BbvnRUyEaTI6bmVx6daqqShytmvl0HB>`_ is a tutorial to guide participants through an 8-step introduction to the Lubuntu 16.04 operating system used for most class computing exercises.

\

2. A list of useful `Linux commands <https://drive.google.com/open?id=17LksoyHNWWac50e17mk_ZEdwEie5E55H>`_ is available as a handy reference.

\

3. The example files for the week1 `quiz <https://drive.google.com/open?id=1lT1CT2uRF1GSiIpPOdG_4mTWZ6Fa7bwb>`_ are at `quiz_week1.tgz <https://drive.google.com/open?id=1J7h4u3YaBrozBAK30lL8K3ekDjAv-2P9>`_ or `quiz.week1_download_script <https://drive.google.com/open?id=1rvbkjygO4P012W9JJUg7D0WZ3Vz12wi1>`_.

\

4. Some links to useful websites with more information about Linux and the bash shell: `The BashGuide <http://mywiki.wooledge.org/BashGuide>`_, `An A-Z Index of the Bash Command Line <https://ss64.com/bash/>`_, and `LinuxCommand.org <http://linuxcommand.org/index.php>`_.



Additional Resources
********************


Background information about Linux:
-----------------------------------

+ A reminiscence called `The Strange Birth and Long Life of Unix <http://faculty.salina.k-state.edu/tim/unix_sg/_downloads/The_Strange_Birth_and_Long_Life_of_Unix_IEEE_Spectrum.pdf>`_ by Warren Toomey in 2011 commemorated the 40th anniversary of the beginning of Unix (and therefore, Linux) development.

\

+ The `Software Carpentry <https://software-carpentry.org/lessons/>`_ website has a series of tutorials with introductions to many aspects of Linux computing. The lessons entitled The Unix Shell and Programming with R are particularly relevant to this course, because we use the shell a lot throughout the course, and R is important in the section on transcriptome analysis.

\

+ Analysis of Next-Generation Sequencing Data workshops (ANGUS) have been taught at Michigan State in the past, and in 2017 moved to UC-Davis. Course materials are available online. The class uses cloud computing instances that are configured differently, so the exercises won't necessarily work exactly the same on the VCL machine image we are using, but the course materials do contain useful information about bioinformatics applications and tools.

\

+ More information on regular expressions is available at `A Brief Introduction to Regular Expressions <http://tldp.org/LDP/abs/html/regexp.html>`_ at The Linux Documentation Project webpage.

\

+ The `FileGlobbing.pdf <https://drive.google.com/open?id=1rZwW8mynGu1JZiFqaYUYinA5DFMgQmgI>`_ and `RegularExpressions.pdf <https://drive.google.com/open?id=1uPppomFXdjnmTJczgnglb8lsoCde-Zic>`_ documents also provide more information on these pattern-matching tools.

\

+ The `LocaleSettingDetails.pdf <https://drive.google.com/open?id=1Ummb6jYkrAindo8riOJr7YuMd4KAV4EV>`_ document covers localization options in UNIX, including the 'C' locale, and how it may affect alphabetical processes.

\

+ One aspect of command-line use is knowing when to use a particular command, and when it is not needed.  Many command-line utilities such as grep, cut, wc,  sort,  sed, and awk (among many others) accept filenames as arguments after the command, but will also accept input from stdin via a pipe. Other utilities, such as tr, do not accept a filename as an argument and only process data received from stdin. Some people prefer to use the cat command to put data into a pipeline, even when the command being used could read the filename as an argument, simply for the sake of consistency and style (see this `StackOverflow discussion <https://stackoverflow.com/questions/11710552/useless-use-of-cat>`_ as an example), while purists argue that using a command when it is not required means running two processes when one will do. This is rarely a problem, but can lead to differences in the commands used to accomplish the same result. For example, in chapter 5 of the Biostar Handbook called Ontologies, the section called Understand the GO data includes some manipulations of a file called goa_human.gaf.gz, after downloading the file from the geneontology.org website.

::

	# Uncompress the GO file:
	gunzip goa_human.gaf.gz

	# Remove the lines starting with ! and simplfy the file name:
	cat goa_human.gaf grep -v '!' > assoc.txt

	# The same result could be obtained in a single step using this alternative
	gunzip goa_human.gaf.gz | grep -v '!' > assoc.txt



Windows Subsystem for Linux in Windows 10
-----------------------------------------

+ Windows 10 offers an optional beta-release of Windows Subsystem for Linux, which allows running any of three different Linux-like command-line environments  on Windows, although the Linux kernel itself is not installed. These provide a command-line bash shell environment with GNU utilities - see a `tutorial on set-up <https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/>`_ or a `Microsoft page <https://docs.microsoft.com/en-us/windows/wsl/install-win10>`_.



Setting up an Amazon Web Service account to use Elastic Compute Cloud services:
-------------------------------------------------------------------------------


+ A 2013 `guide <https://drive.google.com/open?id=1usJgvhq3xdtWNLp514ievfbWubsebaUS>`_ to setting up an Amazon Web Services account is available for those interested in using cloud-based computing resources, and a 2013 `guide <https://drive.google.com/open?id=1z0LqYJUchs6Ozo-R88EyaQReYB4c4MVX>`_ to preparing and running a Cloudbiolinux instance on the Amazon Web Services Elastic Compute Cloud (AWS-EC2), is also available. The BIT815 course no longer uses AWS resources, so these documents have not been updated to reflect any recent changes in AWS procedures – users are cautioned to follow the instructions on the AWS website rather than those in these documents in case of any conflict.






Last modified 11 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
