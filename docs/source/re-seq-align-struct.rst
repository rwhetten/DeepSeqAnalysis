.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Re-sequencing, Alignment, Structural Variation
==============================================


Objective
*********

The objective of this session is to introduce participants to re-sequencing of genomic DNA or cDNA produced from RNA. The term "re-sequencing" indicates that an assembled and annotated genome sequence is available for use as a reference in analysis of the sequence reads. This means that discovery of new sequence information is typically not the primary goal of these experiments. Instead, the sequence reads are used as a measure of some other biological property of interest. A variety of experimental methods have been developed that use massively-parallel DNA sequencing to measure specific aspects of genome structure or transcriptome activity: the accessibility of chromatin to digestion by nucleases, binding of specific proteins to DNA, three-dimensional interactions between chromosomes in the nucleus, and levels of gene expression are some examples of properties that can be measured in this way. After data preprocessing and quality control, alignment of reads to the reference genome sequence provides results in the form of Sequence Alignment and Mapping (SAM/BAM) format alignment files, which are then processed by additional software tools to produce the measurements of experimental interest.


Description
***********

Alignment of short DNA sequence reads to a genome reference sequence can be done by several approaches. One is to produce a "hash table", either of the sequence reads or of the reference genome sequence. A hash table consists of key - value pairs, where the key is a short DNA sequence (a *k-mer*) and the value is the number of times that sequence occurs in the reference genome or the sequence reads. This hash table can then be used to compare sequence reads to the genome to identify regions of the genome that most closely match the DNA sequence in each read. An alternative approach relies on a mathematical transformation called a Burrows-Wheeler Transform, which allows construction of an index of the reference genome sequence. This index is then used to identify the genomic location to which each sequence is most similar.  We will not delve into the mathematics of these methods; see the Wikipedia page on `short read alignment software <http://en.wikipedia.org/wiki/List_of_sequence_alignment_software#Short-Read_Sequence_Alignment>`_ for links to many different alignment programs. 


Key Facts
*********

The length and number of repetitive sequences in a particular genome determine the sequencing strategy to produce data likely to allow a relatively complete assembly, and also help determine the best strategy for detecting variation among individuals in genome sequence. Short-read sequencing is very useful for detecting substitutions or insertion/deletion events (indels) of one to a few basepairs, but is not as sensitive for detecting larger indels (>50 bp), or rearrangments such as inversions, translocations, or duplications. Long-read sequencing has much greater sensitivity for detecting these larger-scale phenomena, but is still a relatively new approach for structural analysis of genomes of higher eukaryotes because of the higher relative cost of long-read methods relative to Illumina sequencing. This cost structure is changing with the increases in the accuracy and yield of reads from PacBio and Oxford Nanopore Technologies instruments. A recent comparison of software designed to detect structural variation in short read resequencing data (`Cameron et al, 2019 <https://www.nature.com/articles/s41467-019-11146-4>`_) concluded that programs designed to do local reassembly of reads around regions of putative structural variation give better results than programs based on other algoriths. An in-depth study in Drosophila comparing the number of structural variants caused by transposable elements using short-read resequencing data versus long-read de-novo genome assembly reported that de-novo genome assembly detected hundreds more variant sites in regions that could be recognized as comparable between the reference assembly and their two new assemblies (`Ellison and Cao, 2019 <https://academic.oup.com/nar/article/48/1/290/5637587>`_). While comprehensive analysis aimed at identifying all structural variants among a group of genomes will probably be best done by de-novo genome assembly with long reads and other data types, it may be possible to survey a subset of structural variation more cost-effectively using short read data given the appropriate data types and software tools. Linked-reads, as produced from libraries made using 10x Genomics Chromium method, the BGI stSLR method, Universal Sequencing's TELL-Seq kit, or the method of `Redin et al (2019) <https://www.nature.com/articles/s41598-019-54446-x>`_, can be used to detect structural variation, with advantages relative to standard short read data in sensitivity and relative to long-read sequencing in cost-effectiveness (`Elyanow et al, 2018 <https://academic.oup.com/bioinformatics/article/34/2/353/4590027>`_, `Zhang et al, 2020 <https://academic.oup.com/nargab/article/2/1/lqz018/5661105>`_)


Variant discovery/genotyping
----------------------------

+ SNPs vs structural variants: SNPs are usually more abundant in terms of numbers of sites, but indels and rearrangement events can affect more nucleotides genome-wide. A report in Nature Genetics (`Chiang et al, 2017 <http://www.nature.com/ng/journal/vaop/ncurrent/full/ng.3834.html>`_) suggests that structural variants often have larger effects on relative expression levels of nearby genes than do SNPs.

\

+ Common alleles vs rare: common alleles are easier to detect and effects can be estimated accurately; rare alleles can be so hard to find that specific strategies are needed to identify sufficient numbers of individuals to provide statistical power to estimate SNP effects

\

+ In-read barcoding of individual samples, as is common in GBS or RAD-seq approaches, works well for genotyping specific individuals at SNPs with common alleles: sequencing pooled samples without individual IDs works well for identifying rare variants and estimating allele frequencies. 

\

+ Many software packages are available for identifying structural variants in alignments of short-read (usually Illumina) sequence data to a reference genome (`Alkan et al, 2011 <https://www.nature.com/nrg/journal/v12/n5/full/nrg2958.html>`_). `Layer et al (2014) <https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-6-r84>`_ describe Lumpy, a program that detects structural variation in whole-genome sequencing data by synthesizing information from different kinds of read alignment results - split reads (where a single read aligns to two different locations), discordant read pairs (where the paired-end reads from a single fragment align to locations inconsistent with that expected based on the fragment sizes in the sequencing library), or differences in read depth (due perhaps to variation in copy number of a particular sequence in the sample genome relative to the reference). A more recent publication by `Becker et al (2018) <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1404-6>`_ describes a Python tool for structural variant detection that uses an ensemble of different structural variant detection programs - BreakDancer (`Chen et al, 2009 <https://www.nature.com/articles/nmeth.1363>`_, BreakSeq (`Lam et al, 2010 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2951730/>`_, cnMOPS (`Klambauer et al, 2012 <https://academic.oup.com/nar/article/40/9/e69/1136601>`_), CNVator (`Abyzov et al, 2011 <https://genome.cshlp.org/content/21/6/974.long>`_), Delly (`Rausch et al, 2012 <https://academic.oup.com/bioinformatics/article/28/18/i333/245403>`_), Hydra (`Quinlan et al, 2010 <https://genome.cshlp.org/content/20/5/623.long>`_), and Lumpy. An extension of this approach (`Zarate et al, BioRxiv 2018 <https://www.biorxiv.org/content/biorxiv/early/2018/09/23/424267.full.pdf>`_) uses parallelization to run some or all of the SV callers BreakDancer, BreakSeq, CNVnator, Delly, Lumpy, and Manta (`Chen et al, 2016 <https://www.ncbi.nlm.nih.gov/pubmed/26647377>`_), on a multi-core computer in roughly the same time required to run a single program. Two comparison of results from different software tools have recently been published; one reported results from 69 different packages (`Kosugi et al, 2019 <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1720-5>`_), while another comparison selected a subset of 10 programs based on different algorithms or combinations of algorithms (`Cameron et al, 2019 <https://www.nature.com/articles/s41467-019-11146-4>`_). The latter paper reports, perhaps not surprisingly, that one of the better programs for detection of structural variants in Illumina short read data is Gridss, a software package previously described by the same research group (`Cameron et al, 2017 <https://genome.cshlp.org/content/27/12/2050>`_)

\

+ Efficient analysis of data from population-level whole-genome sequencing projects in humans is essential, due to the size of the human genome and the computational intensity of sequence alignment and variant detection. `Johnston et al (2017) <http://www.pnas.org/content/114/10/E1923.full>`_ describe two new programs, PEMapper and PECaller, to improve the efficiency of these analyses. `Smith et al (2017) <https://academic.oup.com/gigascience/article/6/10/1/4160384>`_, describe the Genome Rearrangement Omni Mapper (GROM) program to efficiently identify all classes of sequence variation including SNPs, structural variants, indels, and copy-number variants.

\

+ `Firtina & Alkan (2016) <https://academic.oup.com/bioinformatics/article/32/15/2243/1743552>`_ report that changing the order of sequence reads in a FASTQ file, followed by alignment of the reads to the human reference genome and SNP calling with various software tools shows discordance in identified variants, ranging from less than 1% to around 25%. This observation suggests that any variant-calling routine should be tested for sensitivity to read order in the input FASTQ files, although for large datasets this repeatability analysis would be extremely time-consuming.

\

+ Variant normalization, or reconciling differences in alignments and SNP or indel calls in low-complexity regions, is an important topic for researchers interested in making a complete catalog of genetic variation in a population. A seminal paper by `Tan et al (2015) <https://www.ncbi.nlm.nih.gov/pubmed/25701572>`_ introduced software for variant normalization using a VCF file and the reference sequence.  `Bayat et al (2017) <https://www.ncbi.nlm.nih.gov/pubmed/27993787>`_ reported additional concerns regarding the normalization algorithm used by other software and offered another software package they believe does a better job.


\


Exercises
*********

1. Data suitable for Gridss analysis, derived from a *Drosophila melanogaster* resequencing experiment, are available for download:  `reference genome archive <https://drive.google.com/a/ncsu.edu/file/d/18wFOo9cWuL30k2QBnQz_Ib9k3sDb2Tss>`_,    `blacklist file <https://drive.google.com/a/ncsu.edu/file/d/1bz6C8s9cT1qKpDkLUKDQNVaGSRxxwPqg>`_, and  `reads.bam file <https://drive.google.com/a/ncsu.edu/file/d/1d5RInRtVI4vWslTOrf-Tb6WE06fXi-bX>`_  (or if you are having issues downloading the bam file use `this link <https://drive.google.com/open?id=1fGMzJ7tmVOpH3-QpASeuLdy87eEq5hz3>`_) of Illumina reads aligned to the reference genome. These reads are from Sequence Read Archive accession SRR2033228 - the reason for providing the BAM file rather than the raw read data is to save the considerable time required to align the reads to the reference genome. `Notes <https://drive.google.com/a/ncsu.edu/file/d/1Zgcd_nQtr1w9T3628Dn00EI773Mb7kcu>`_ are also available describing the steps in preparing the BAM file and running Gridss.

\

2. Erik Garrison, lead author of the Freebayes SNP caller, has an `exercise in alignment and variant calling <https://github.com/ekg/alignment-and-variant-calling-tutorial>`_ on his Github page, using both E. coli and human datasets downloaded from web sources. The software required for this tutorial is installed in the VCL machine image. A set of `slides <https://drive.google.com/open?id=1XR3kHmCQrTMs007oFKyMs-Qo04lW30vU>`_ from a presentation Garrison gave in 2015 describing the Freebayes SNP caller and how it is used in the 1000 Genomes project exploring human genome diversity are also available.

\

3. Data from an exercise presented at a `2016 Canadian bioinformatics workshop <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/>`_ are in `Module3.tar.gz <https://drive.google.com/open?id=1KZGdzI50VadXdbnhC3BznAuek3eiXEJx>`_. You can directly download the module archive with the following terminal command in an SSH session:
::

	ggID='1KZGdzI50VadXdbnhC3BznAuek3eiXEJx'; echo "The file ID is $ggID"; ggURL='https://drive.google.com/uc?export=download'; filename="$(curl --insecure -sc /tmp/gcookie "${ggURL}&id=${ggID}" | grep -o '="uc-name.*</span>' | sed 's/.*">//;s/<.a> .*//')"; getcode="$(awk '/_warning_/ {print $NF}' /tmp/gcookie)"; curl --insecure -LOJb /tmp/gcookie "${ggURL}&confirm=${getcode}&id=${ggID}"

\

Web pages describe the steps required to `align samples <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/mapping>`_ of reads from normal and tumor samples to a reference human genome sequence, then analyze the resulting alignments to `identify rearrangements <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/rearrangement>`_. Before executing this exercise, you must create a "virtual environment" in which you install Python v2.7 and the numpy (Numerical Python) module, because the Lumpy program relies on those dependencies. Create the virtual environment with 

:code:`conda create --name=py2 python=2.7` 

- you will have to respond to a question confirming the installation. After creation of the virtual environment is complete, activate the environment using 

:code:`source activate py2` 

- you will see that the prompt changes to include (py2), so you can tell from the terminal prompt which virtual environment is in use. Install the numpy module in the terminal window running the virtual environemtn, using 

:code:`conda install numpy` 

- this will also ask for confirmation. Normally the creation of a virtualenv and installation of modules would only need to be done once, but because everything in the home directory is lost when a VCL instance is shut down, these steps must be repeated with each new instance that is started.

\

3.1. Download a `shell script <https://drive.google.com/open?id=1CTWJGeBctKpQ7XFgsVcK9UP7nFU9y2Vj>`_ that will carry out the commands given in the webpages linked above, edited to reflect the differences in file paths and configuration of the VCL instance using 
::

	ggID='1CTWJGeBctKpQ7XFgsVcK9UP7nFU9y2Vj'; echo "The file ID is $ggID"; ggURL='https://drive.google.com/uc?export=download'; filename="$(curl --insecure -sc /tmp/gcookie "${ggURL}&id=${ggID}" | grep -o '="uc-name.*</span>' | sed 's/.*">//;s/<.a> .*//')"; getcode="$(awk '/_warning_/ {print $NF}' /tmp/gcookie)"; curl --insecure -LOJb /tmp/gcookie "${ggURL}&confirm=${getcode}&id=${ggID}"
 

------------------
	
**IMPORTANT NOTES**

	The full human reference genome sequence is too large to work in the alignment step, so after you unpack the Module3.tar.gz archive, you will need to change into the Module3 directory and extract the reference sequences for chromosomes 3, 6, 9 and 12 (because those have rearrangements on them) to a new file. The module3.sh script includes the command 
::

	bioawk -cfastx '{if($name==3 || $name==6 || $name==9 || $name==12) {print ">"$name"\n"$seq}}' human_g1k_v37.fasta | fold | gzip > chr36912.fa.gz

\	
			to do this extraction; other ways are possible as well. The process will take a few minutes, so don't assume that something is wrong if you don't get a terminal prompt back right away after entering this command.

			After extracting the subset of 4 chromomes from the complete reference genome, the script will delete the files related to the complete human genome reference sequence and index files, to free up disk space.
			The next step is to create a BWA index before aligning reads to the four chromosomes of interest. The script uses the command 

::

	bwa index -p subset chr36912.fa.gz

\

		to create an index with the name 'subset'. This will take several minutes, so don't be impatient.



\

3.2. Map the normal tissue-derived and tumor-derived reads back to the reference genome sequence, piping the SAM-format output from the BWA mem aligner to samtools sort to sort the BAM file by reference position so alignment viewers can efficiently display the resulting alignments. The module3.sh script uses the following command line:

 ::

	bwa mem -t8 -p subset reads.tumour.fastq | samtools sort -o tumour.bam - 


\



	The alignment will take a few minutes for the tumor-derived reads. A modified version of the same command is used to align the normal-tissue-derived reads to the same reference, convert the output to BAM, and sort the output BAM file. After both BAM files are complete, the script uses the samtools index command to produce index files for each of them. If you don't know how to use the samtools index command (and no one is born knowing this sort of thing), try typing :code:`samtools index -h` at a terminal prompt to see what information is available, or do a Google search.


\



3.3. The command to produce files of discordant reads from the BAM alignments uses the "flag" column of SAM format, which is a numerical value that contains answers for 12 different yes-or-no questions. The `Explain SAM flags <https://broadinstitute.github.io/picard/explain-flags.html>`_ web page has a list of the 12 properties of reads that make up the flag value; if the value 1294 is entered in the box, the corresponding properties of the reads are identified. The samtools view -F1294 option means "do not show reads with flags containing any of these values", effectively excluding reads with the checked characteristics from the ouput.

\

3.4. The command to produce files of split reads uses a script called extractSplitReads_BwaMem in the scripts subdirectory of the Module3 directory - make sure you use the correct path when you try to execute this command, and pay attention to the permissions on the files in the scripts subdirectory. How can you change the permissions to allow execution of all those script files?

\

3.5. The LUMPY program is installed in the VCL machine image and the path to the executable program is in the search PATH variable, so you should be able to execute that program without concern about what path to use to the program. The paths to the input files, and the names of the input files, however, must match those present on your instance of the machine image.


Additional Resources
********************

+ Information on the Sequence Alignment and Mapping (SAM) format is available at a University of Michigan `wiki <https://genome.sph.umich.edu/wiki/SAM>`_, at `Dave’s Wiki <https://davetang.org/wiki/tiki-index.php?page=SAM>`_, and in the SAM format `specification <https://samtools.github.io/hts-specs/SAMv1.pdf>`_. 

\

+ Quality control of alignment files is a valuable preliminary step before investing significant time and effort in analysis. A package called *indexcov* is available to efficiently summarize coverage of different genomic regions within a single sample, or uniformity of coverage across multiple samples, beginning with alignments in BAM or CRAM formats. See Indexcov: fast coverage quality control for whole-genome sequencing. `GigaScience 6:1-6, 2017 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5737511/>`_

\

+ Genomic rearrangements in Arabidopsis considered as quantitative traits. `Imprialou et al, Genetics 205:1425-1441  <http://www.genetics.org/content/205/4/1425>`_, 2017. *This paper describes a strategy for mapping likely locations of structural rearrangements in a segregating population of recombinant inbred lines using low-coverage (0.3x) whole-genome resequencing.*

\

+ LUMPY: a probabilistic framework for structural variant discovery. `Chiang et al, Genome Biology 15:R84, <https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-6-r84>`_ 2014.

\

+ CNVnator: An approach to discover, genotype, and characterize typical and atypical CNVs from family and population genome sequencing. Abyzov et al, `Genome Research 21: 974-984, <http://genome.cshlp.org/content/21/6/974.full>`_ 2011.

\

+ Canvas: versatile and scalable detection of copy number variants. Roller et al., `Bioinformatics  32: 2375-2377, <https://academic.oup.com/bioinformatics/article/32/15/2375/1743834/Canvas-versatile-and-scalable-detection-of-copy>`_ 2016.

\

+ Genome structural variation discovery and genotyping. Alkan et al, `Nature Reviews Genetics 12:363-376, <http://www.nature.com/nrg/journal/v12/n5/full/nrg2958.html>`_ 2011.




Last modified 4 February 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
