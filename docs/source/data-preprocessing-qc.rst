.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: red

.. role:: underline
   :class: underline

.. role:: bash(code)
   :language: bash

Data Preprocessing and Quality Control
======================================

Global Overview
***************

Data from high-throughput DNA sequencing platforms (such Illumina, Ion Torrent, Pacific Biosciences, or Oxford Nanopore) can contain a variety of experimental artifacts and low-quality data, so quality control and data pre-processing are always a good idea. Common artifacts in sequences from Illumina and Ion Torrent instruments include copies of the adapter sequences, because these instruments use solid-phase PCR to amplify the template DNAs using in the sequencing reaction. FASTQ-format data contains both the DNA sequence data and an estimate of the probability of error for each base in the sequence; removing sequences (or regions of sequences) consisting of low-quality base calls is another common pre-processing step. The stringency of such quality-filtering or trimming steps can affect the results of downstream data analyses, and the optimal level of stringency for filtering or trimming may be different for different downstream analyses. For example, RNA-seq analysis of differential gene expression can be biased by too-stringent quality trimming (`MacManes, 2014 <https://www.frontiersin.org/articles/10.3389/fgene.2014.00013/full>`_; `Williams et al, 2016 <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-016-0956-2>`_) 

Objective
*********

The objective of this session is to provide participants with experience in managing and processing DNA sequence data. A review of FASTQ format will be followed by practical exercises in data quality analysis with FastQC and data filtering with tools from the BBTools suite.

Description
***********

The most common format for sequence data output from high-throughput instruments is FASTQ format (Cock et al., 2010), containing sequences coupled with their quality stored as text characters. The quality scores are -10 times the logarithm (to base 10) of the per-base probability of an incorrect nucleotide call at each position in the sequence, and are based on the PHRED quality score (Ewing and Green, 1998; Ewing et al., 1998). In the past, some instruments produced separate files containing DNA sequences (in Fasta format) and quality scores (*.qual files), so you may encounter these file formats as well.  The numerical quality scores (typically ranging from around zero to around 40) are converted into single characters to save space. A two-digit quality score must be followed by a space to distinguish it from the score for the next nucleotide, so one value requires three characters, while a single text character contains the same information and need not be separated by a space from the next single character.

Unfortunately, multiple different conventions have been used for encoding quality data in text characters using the American Standard Code for Information Interchange (ASCII), and knowing which convention was used for any given dataset is important. The Wikipedia page on `FASTQ format <https://en.wikipedia.org/wiki/FASTQ_format>`_ is the most up-to-date source of information about the different encoding schemes used in the past and the current encoding used by Illumina instruments (called Illumina 1.8+ in the figure).

Several tools for summarizing the frequency and identity of contaminating adapter sequences and the distribution of quality scores per base or per sequence are available; we will use the Java program FastQC for data quality summaries. Many different software tools exist for removing low-quality base calls from the 5' end or 3' ends of sequence reads, for trimming off sequencing adaptor sequences or other extraneous sequences, and for separating reads from a single dataset into multiple datasets based on the presence of "barcode" sequences at the beginning of the sequence reads. We will use both fastx-toolkit (a simple, lightweight but limited toolset) and BBTools (a Java-based and extremely comprehensive package of programs) for trimming and filtering reads.

Key Facts
*********

DNA sequence data as produced from the instrument can vary in quality and read length, and some exploratory analysis and filtering of the data is essential before beginning the process of analyzing the sequence to achieve  experimental objectives. Understanding the format in which sequence data are provided is essential, as there are (unfortunately) multiple versions of the "standard" FASTQ format in use.  Converting FASTQ format to FASTA is simply a matter of stripping out the quality data and changing the character at the beginning of the sequence header line, but converting FASTA and quality score files into a single FASTQ format file requires converting numerical quality scores into characters using the ASCII lookup table.

Exercises
*********

1. Sequence format conversion tools. The key difference between FASTA and FASTQ format is that FASTQ contains quality scores. If you have a FASTA file containing sequences, and no accompanying file of quality scores, there is no meaningful way to provide real quality scores for creation of a FASTQ file.  If you have a separate .qual file of quality scores, you can use various tools to merge the FASTA sequences with the quality scores to produce a FASTQ format file. Search online for a user guide to the BBTools package of programs, which is installed on the VCL machine image and has a reformat.sh script that can perform this conversion as well as many others. Read through the help information to learn about the capabilities of the BBTools package of programs, or see Bushnell et al (2017) for more details on the BBMerge tool from this package that can merge paired-end reads into longer single sequences.

\

2. Software: fastx-toolkit and FastQC. `FastQC <https://www.bioinformatics.babraham.ac.uk/projects/fastqc/>`_ is a Java program that will run on Windows, Mac, or Linux, and is already installed on the VCL machine image - the link here is provided for those interested in installing the software on another machine. The fastx-toolkit package of programs is available in the Ubuntu repository, and is also already installed on the machine image.  These programs differ in that FastQC has a nice graphic interface and produces pretty graphs describing various aspects of data quality, but has no capability to filter, trim, or otherwise modify sequence files to address problems made apparent in those pretty graphs. The fastx-toolkit package can also produce graphs, although they aren't quite as pretty, but it does include programs capable of filtering and trimming sequence data files.

\

3. Using fastx-toolkit for exploratory analysis. The first exercise will use fastx-toolkit to analyze and process the `c3.fq.gz <https://drive.google.com/open?id=1DhVkPmszlpvH8dIKXef2iiSO-cF_cj-v>`_ sequence file, also found in the the `fullset.zip <https://drive.google.com/open?id=16W-W3t3DILI05cufENJRq8NnO1vz7mge>`_ archive. The fastx-toolkit programs are simple and somewhat dated, but still useful. Download the `QCexercises.sh <https://drive.google.com/open?id=1ERJJYdJciiw0Z3q0LDUfm-QGPcwpdxrB>`_ shell script with exercises.

\

4. Run the script using the command bash `QCexercises.sh <https://drive.google.com/open?id=1ERJJYdJciiw0Z3q0LDUfm-QGPcwpdxrB>`_ from a terminal prompt. The shell script should create two image files (with a .png extension) in the directory where you run it - use one of the image viewer programs available under Graphics in the Application menu of the Linux system to view these image files, or just use the display command at a terminal prompt.

::

  display c3.qual.png &



\


5. Open the `QCexercises.sh <https://drive.google.com/open?id=1ERJJYdJciiw0Z3q0LDUfm-QGPcwpdxrB>`_ file with the Geany programming text editor (listed under the Development item in the Applications menu)  and read the code and comments to learn what the script does. You can run the script multiple times with different input sequence files, changing the name of the file to be used as input to the series of programs, or you can simply copy the commands from the script file to a terminal window and run each command from the command line, one step at a time.

\

6. Run FastQC on the same file, and compare the results. FastQC produces a report containing an HTML file that can be opened using a browser. By default FastQC tries to write the output to a directory in the same place where the sequence file is found - you must have write permission in that directory. You can specify an alternative place to save the output using the -o option on the command line.

::

  fastqc -o ./ c3.fq.gz

The resulting HTML output file can be opened with a browser from the command line; e.g.::

  palemoon c3_fastqc.html

7. Using fastx-toolkit to remove adaptor sequences and trim off low-quality bases. Find the web page with instructions on the individual programs in the fastx-toolkit package (remember, the information is out there - you just have to find it). Use the fastx_clipper and fastq_quality_filter programs to remove any copies of the Illumina sequencing adaptor (GATCGGAAGAGCTCGTATGCCGTCTTCTGCTTGAAA) and to trim low-quality bases so that 80% of the bases in each read have a quality score of 15 or higher. Note that the fastx-toolkit programs accept input from STDIN and deliver output to STDOUT by default, so they are designed to be linked together in pipelines for processing data without the need to save intermediate files. See the `QCexercises.sh <https://drive.google.com/open?id=1ERJJYdJciiw0Z3q0LDUfm-QGPcwpdxrB>`_ script file for an example of how to format the command to send decompressed fastq-format sequence to fastx-toolkit commands.

**NOTE: the -Q33 option is required** - fastx-toolkit by default assumes that fastq-format sequences have quality scores from an older version of the Illumina base-calling software, and if you don't tell it to use the new version, it will return an error message.

\

8. :underline:`Using BBTools programs to remove adaptor sequences and trim low-quality bases.` The BBTools programs are installed in the /usr/local/bbmap directory of the Linux system, and this directory has been included in the $PATH environment variable, so you can run them by typing the name of the command at a terminal prompt, for example bbduk.sh to run the bbduk.sh program. Executing this command with no arguments will print a user guide for the command to the terminal screen, so this is one way to learn what options and arguments each command accepts. A web search will lead you to a BBTools User Guide at the DOE Joint Genome Institute, because the author (Brian Bushnell) is a bioinformatics specialist at JGI. NOTE: many of the BBTools programs are Java-based, so they can  be used on any operating system that has Java installed, but you can read the user guides for all the commands without installing Java. By default, the bbduk.sh and bbduk2.sh programs do not use the same sliding window approach for quality trimming as does fastq_quality_filter, but setting the appropriate options during execution of either bbduk.sh or bbduk2.sh will allow that approach to be used. For more information about alternative ways of quality trimming, see this `SeqAnswers Forum <http://seqanswers.com/forums/showthread.php?t=42776&page=7>`_ thread, and look for post #134.

\

9. :underline:`Summarizing sequence data characteristics using FastQC.` You can run FastQC either from the command line, providing the names of sequence files to be processed as arguments, or from a graphic user interface. Typing the  command :code:`fastqc` without providing an input filename will start the program in interactive mode, where you choose which file to analyze from the File menu, while providing a file "glob" using wildcard characters will run the program on every sequence file that matches the filename pattern from `fullset.zip <https://drive.google.com/open?id=16W-W3t3DILI05cufENJRq8NnO1vz7mge>`_, e.g.

::

  fastqc /fullset/[ct][123].fq.gz



Note that the FastQC program can process gzip-compressed sequence files without saving an uncompressed version - this is important for saving disk space when hundreds of gigabytes of compressed sequence files need to be processed.




Additional Resources
********************

+ Wikipedia has information on `FASTA <http://en.wikipedia.org/wiki/Fasta_format>`_ and `FASTQ <http://en.wikipedia.org/wiki/Fastq>`_ sequence formats.

\

+ The University of California - Santa Cruz Genome Browser site maintains a `FAQ <http://genome.ucsc.edu/FAQ/FAQformat.html>`_ with information about many different file formats used in analysis of deep sequencing data

\

+ The fastx-toolkit `webpage <http://hannonlab.cshl.edu/fastx_toolkit/commandline.html>`_ has information about the fastx-toolkit package of programs for quality control and manipulation of FASTA and FASTQ files.

\

+ The FastQC `webpage <http://www.bioinformatics.babraham.ac.uk/projects/fastqc>`_ has information about the FastQC program, and details on FastQC output are provided in the `FastQC_details.pdf <https://drive.google.com/open?id=1L9SSnfDTVgP8EeqHZGZe5gG4EHH8xRMT>`_ document.

\

+ Another program suitable for adapter trimming is called "flexbar" - this program can also split reads into different files based on the presence of specific "barcode" sequences detected in the sequence reads. Such barcodes are common in GBS and RAD-seq applications, and the ability to detect variable-length barcodes is somewhat unusual. The manual for flexbar is on `Sourceforge <http://sourceforge.net/p/flexbar/wiki/Manual/>`_, and the `publication <http://www.mdpi.com/2079-7737/1/3/895>`_ describing the software is also available.

\

+ The BBtools suite of programs was announced on the SeqAnswers forum, and the correspondence between the program developer and users is archived as a resource for others to learn how to use the various tools in the suite. The announcements and correspondence are in separate threads for individual programs; the `list of tagged posts <http://seqanswers.com/forums/tags.php?tag=bbtools>`_ can be viewed to see links to the individual threads. The software is available at the Sourceforge `project page <https://sourceforge.net/projects/bbmap/>`_.

\

+ Breese MR, Liu Y. (2013) NGSUtils: a software suite for analyzing and manipulating next-generation sequencing datasets. Bioinformatics 29: 494-496, 2013. `PMID 23314324 <http://www.ncbi.nlm.nih.gov/pubmed/23314324>`_ (***Note**: This paper describes a set of software tools for managing the process of data QC and format conversion, including tools for filtering datasets of paired-end reads to find single reads where the paired-end read was removed by a quality-filtering step*).

\

+ Cock PJ, Fields CJ, Goto N, Heuer ML, and Rice PM. (2010) The Sanger FASTQ file format for sequences with quality scores, and the Solexa/Illumina FASTQ variants. Nucleic Acids Res. 38: 1767–1771. `PMID 20015970 <http://www.ncbi.nlm.nih.gov/pubmed/20015970>`_ (***Note**: This is the only formal publication I know of that describes the different versions of the FASTQ sequence format, and it is not as up-to-date as the Wikipedia page on FASTQ format*).

\

+ Ewing B, Hillier L, Wendl MC, Green P (1998). Base-calling of automated sequencer traces using phred. I. Accuracy assessment. Genome Res. 8 (3): 175–185. `PMID 9521921 <http://www.ncbi.nlm.nih.gov/pubmed/9521921>`_

\

+ Ewing B, Green P (1998). Base-calling of automated sequencer traces using phred. II. Error probabilities. Genome Res. 8 (3): 186–194. `PMID 9521922 <http://www.ncbi.nlm.nih.gov/pubmed/9521922>`_



Last modified 17 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
