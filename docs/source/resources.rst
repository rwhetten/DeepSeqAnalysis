.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Course Resources
================

Introductory Concepts and Vocabulary
************************************

The world of command-line Linux has a specialized vocabulary that is second nature to those who work in that world, but can be a barrier to those without a background in computer science or programming. The first three chapters of Eric Raymond's book `The Art of Unix Programming <http://www.catb.org/esr/writings/taoup/html/>`_ provide an introduction to the philosophy underlying the Unix and Linux operating systems, a brief history, and some comparisons among operating systems to help new users understand some important differences between Linux and other operating systems.

One key difference between open-source Linux and closed-source commercial operating systems is the modular nature of Linux. A Linux operating system is a collection of individual programs that work together to provide the desired functionality for a user, and Linux recognizes that different users desire different functionalities. A Linux distribution is a package of programs selected to work together to provide core functions, but users are free to add additional programs with new functions to meet their specific needs. This has to be done in an organized way, to assure that the added programs are compatible with the core functions of that distribution, so it is common for distributions to maintain repositories of programs that are suitable for installation. For example, the Debian family of Linux distributions (98 derivative distributions as of Jan 2018, per the `Debian Wiki <https://wiki.debian.org/Derivatives/Census>`_ webpage) use a program called apt (Advanced Package Tool) to manage packages. The command **apt-cache dump | grep -c "^Package:"** yields a count of over 112,000 packages in the repositories for Ubuntu, one of the "children" of the Debian distribution. Many of these are components that work together, while others are redundant or provide overlapping functions, so no single system would need to have all of them installed, but they are available to allow users to configure a Ubuntu-based system to meet their own needs.

Many of the programs used for bioinformatics are available in Debian or Ubuntu repositories, which is one reason why this family of distributions is popular with users of such programs. Searching the respository is a good first step to take when the need arises to install a particular bioinformatics tool. For example, Bio-Perl is a set of specialized modules in the Perl scripting language that provide capabilities for DNA and protein sequence analysis and other bioinformatics tasks, and this tool is often utilized by other bioinformatics programs that depend upon these specialized capabilities. Executing the command **apt-cache search bioperl** on the command line of an Ubuntu-based Linux system shows that there are several packages related to Bio-Perl in the Ubuntu repositories. It is often true that the most recent versions of software are not available in the repositories, so if you need a specific recent version of a particular program (perhaps because another program depends on new functions introduced in that version), you may have to install from source rather than from the repository.


Cartoons about biology or computing from xkcd
*********************************************

+	`DNA as source code <https://xkcd.com/1605/>`_
+	`tar command <https://xkcd.com/1168/>`_
+	`the power of sudo <https://xkcd.com/149/>`_


Resources about the Linux command-line environment and the Bash shell
*********************************************************************

+	`Greg's Wiki BashGuide <http://mywiki.wooledge.org/BashGuide>`_ provides a good introduction to the fundamental concepts of the command line interface, including sections on regular expressions, variables and arrays, tests and conditionals, job control, and scripting.

+	The `Advanced Bash Scripting Guide <http://www.tldp.org/LDP/abs/html/>`_ is a comprehensive resource of information about many aspects of Bash programming, and also includes appendices with introductions to awk and sed, which are powerful tools for managing and manipulating text on the command line.

+	`Parameter expansion <http://wiki.bash-hackers.org/syntax/pe>`_ is a wiki page with information about bash parameter expansion, a handy tool for manipulating variables in the bash shell.

+	A `guide <https://drive.google.com/open?id=1oSUePtxotttzn9giJZHHVAldZtyAfr2d>`_ to setting up a computing session on a virtual machine through the NC State Virtual Computing Lab (VCL) is available. This resource is only available to members of the NC State community, because the VCL requires authentication with an NC State user id and password. The work done on a virtual machine instance is lost when the instance is terminated, so if you want to save results of analyses done on a virtual machine, you must either upload the files to a cloud storage site (e.g. Google Drive, Dropbox, velocity.ncsu.edu, or something similar) or mount your AFS file space as an external volume on the virtual machine. To mount AFS as an external volume, first authenticate to the Kerberos server using your NC State user id: **kinit [username]**. A prompt will pop up, asking for your NC State password, but no characters typed at this prompt are echoed to the screen. After your password is accepted, enter the command **aklog** at a terminal prompt to mount the AFS volume. Your personal space will be at the path **/afs/unity.ncsu.edu/users/X/Y**, where X is the initial letter of your user ID and Y is your full user ID.



Advice about bioinformatics from blog posts and papers
******************************************************

+	`Mick Watson <http://www.opiniomics.org/the-five-habits-of-bad-bioinformaticians/>`_ weighs in with an opinion about five bad habits bioinformaticians should avoid.

+	`Ten simple rules for reproducible computational research <http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003285>`_ from Sandve, et al., PLoS Comput Biol 2013.

Links to sequence and alignment data files used in exercises
************************************************************

+	Data from reduced-representation sequencing of the genome of spotted gar are available in `bamfiles.tgz <https://drive.google.com/open?id=1Kku1sschgluviX-xiX8nC_qyLKoCSkB8>`_, a gzipped tar archive containing BAM alignment files for 94 progeny and two parents of a full-sibling family. Only data from linkage group 2 are provided, to keep the file sizes manageable. The reference sequence for the linkage group is available in `LG2.fa.gz <https://drive.google.com/open?id=1tuz5QihPMiOTM_Trdux4gpvRVjAj58tE>`_, and annotation is in `LG2.gff3.gz <https://drive.google.com/open?id=1XL0_tgdBe5ZqkwflT0N2XKipEoHvIsW9>`_. See `Amores, et al, 2011 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3176089/>`_ for a complete description of the experimental design and data.

+	`sampleReadsSAM.tgz <https://drive.google.com/open?id=1m1ZqJYW1r1Q1m8xcfYv_RLlu2HaSwmbw>`_ A gzipped tar archive containing two 100-nt paired-end fastq-format sequence files and a SAM alignment file with results of aligning those reads to a small sample of contigs from a reference transcriptome.

+	`DPC4571.fasta.gz <https://drive.google.com/open?id=1Aj85OISJucpTYg5jwMhhAldwpMAlmzvZ>`_ A gzipped file containing a fasta-format sequence file of the Lactobacillus helveticus strain DPC4571 genome.

+	`OWB_RAD.fastq.gz <https://drive.google.com/open?id=1FCxU6sl8_aM2y9TR9h6JhiTR9yybH-tb>`_ A gzipped file containing fastq-format sequences from an early RAD-seq experiment with the Oregon Wolfe barley lines.

+	`t3.fq.gz <https://drive.google.com/open?id=15XBOf8d9s7kl7mp4Hvi0ETQbe4v4BnpR>`_ A gzipped file containing fastq-format sequences from test sample 3 of the `Cumbie et al <http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0025279>`_ RNA-seq experiment with Arabidopsis, used for data QC, reference-guided transcriptome assembly, and differential gene expression exercises.



Links to useful Wikipedia pages
*******************************

+	`FASTQ format <https://en.wikipedia.org/wiki/FASTQ_format>`_ definition and explanation

+	`FASTA format <https://en.wikipedia.org/wiki/FASTA_format>`_ definition and explanation

+	`K-mer <https://en.wikipedia.org/wiki/K-mer>`_ definition and description on Wikipedia

+	`Sequence alignment software <https://en.wikipedia.org/wiki/List_of_sequence_alignment_software>`_ page, with a fairly comprehensive list of open-source and commercial programs for analysis of DNA sequence data.



Links to other sequence data analysis course materials
******************************************************

+	`ANGUS 5.0 <http://angus.readthedocs.org/en/latest/>`_, the Michigan State University course on Analyzing Next-Generation Sequencing data.

+	`Analyzing Next-Gen Sequencing Data 2013 <http://www.personal.psu.edu/iua1/courses/2013-BMMB-597D.html>`_ slides, homework, and notes from a course taught by Istvan Albert at Penn State

+	`Unix & Perl Primer for Biologists <http://korflab.ucdavis.edu/unix_and_Perl/>`_ an on-line course by Keith Bradnam and Ian Korf at UC-Davis, for biologists interested in learning Unix and the scripting language Perl.

+	`Course <http://ngs-course.readthedocs.io/en/praha-january-2016/>`_ on UNIX and Genomic Data, Prague, Jan 2016 - complete materials, provided by Libor Morkovsky and Vaclav Janousek. The materials include exercises, both in the "Additional exercises" link and in PDFs of course slides under the "Slide decks" link. The slide sets under the "old" heading are from a course taught in April of 2015, and are not out of date.


Links to software pages on Github and Sourceforge
*************************************************

+	`SAMtools and BCFtools <https://github.com/samtools>`_ versions 1.1 and higher, on Github: tools for processing SAM/BAM alignment files and VCF/BCF variant call files.

+	`SAMtools and BCFtools <http://samtools.sourceforge.net/>`_ version 0.1.19 and earlier, on Sourceforge: earlier versions of tools for processing SAM/BAM alignment files and VCF/BCF variant call files.

+	`Flexbar <http://sourceforge.net/projects/flexbar/>`_ on Sourceforge: a tool for barcode-splitting of single-end or paired-end reads, quality filtering and trimming, and adapter removal, with links to download source code and to the manual with complete documentation.

+	`bioawk <https://github.com/lh3/bioawk>`_ on Github: a version of the awk text-processing utility with specific features added to speed processing of biological data files, including BED, GFF, SAM, VCF, and Fasta/Fastq files. This includes the ability to read and write gzipped files, which standard awk cannot do.

+	`Musket <http://musket.sourceforge.net/homepage.htm>`_ on Sourceforge: a multi-stage, k-mer spectrum based error correction program capable of multi-threaded error correction of Illumina short reads.


Last modified 2 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
