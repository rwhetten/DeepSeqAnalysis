.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Re-sequencing, Alignment, Structural Variation
==============================================


Objective
*********

The objective of this session is to introduce participants to re-sequencing of genomic DNA or cDNA produced from RNA. The term "re-sequencing" indicates that an assembled and annotated genome sequence is available for use as a reference in analysis of the sequence reads. This means that discovery of new sequence information is typically not the primary goal of these experiments. Instead, the sequence reads are used as a measure of some other biological property of interest. A variety of experimental methods have been developed that use massively-parallel DNA sequencing to measure specific aspects of genome structure or transcriptome activity: the accessibility of chromatin to digestion by nucleases, binding of specific proteins to DNA, three-dimensional interactions between chromosomes in the nucleus, and levels of gene expression are some examples of properties that can be measured in this way. After data preprocessing and quality control, alignment of reads to the reference genome sequence provides results in the form of Sequence Alignment and Mapping (SAM) format alignment files, which are then processed by additional software tools to produce the measurements of experimental interest.


Description
***********

Alignment of short DNA sequence reads to a genome reference sequence can be done by several approaches. One is to produce a "hash table", either of the sequence reads or of the reference genome sequence. A hash table consists of key - value pairs, where the key is a short DNA sequence (a *k-mer*) and the value is the number of times that sequence occurs in the reference genome or the sequence reads. This hash table can then be used to compare sequence reads to the genome to identify regions of the genome that most closely match the DNA sequence in each read. An alternative approach relies on a mathematical transformation called a Burrows-Wheeler Transform, which allows construction of an index of the reference genome sequence. This index is then used to identify the genomic location to which each sequence is most similar.  We will not delve into the mathematics of these methods; see the Wikipedia page on `short read alignment software <http://en.wikipedia.org/wiki/List_of_sequence_alignment_software#Short-Read_Sequence_Alignment>`_ for links to many different alignment programs. 


Key Facts
*********

The length and number of repetitive sequences in a particular genome determine the sequencing strategy to produce data likely to allow a relatively complete assembly. The objective is to have good coverage of the genome with pairs of reads that are far enough apart to guarantee that both reads of a pair are **not** within the same repetitive sequence element.  If one read is within a repetitive element and the other read is in flanking sequence that is unique in the genome, then that read pair provides evidence locating one copy of the repetitive element within a specific unique-sequence region in the genome. Different genomes have differing lengths and arrangements of repetitive DNA sequences in the genome, so different strategies may be required for library construction and sequencing.


Variant discovery/genotyping
----------------------------

+ SNPs vs structural variants: SNPs are usually more abundant in terms of numbers of sites, but insertion/deletion (indel) and rearrangement events can affect more nucleotides genome-wide. A report in Nature Genetics (`Chiang et al, 2017 <http://www.nature.com/ng/journal/vaop/ncurrent/full/ng.3834.html>`_) suggests that structural variants often have larger effects on relative expression levels of nearby genes than do SNPs.

+ Common alleles vs rare: common alleles are easier to detect and effects can be estimated accurately; rare alleles can be so hard to find that specific strategies are needed to identify sufficient numbers of individuals to provide statistical power to estimate SNP effects

+ Barcoding works well for genotyping specific individuals at SNPs with common alleles: pooled samples work well for identifying rare variants and estimating allele frequencies. 

+ Many software packages are available for identifying structural variants in alignments of short-read (usually Illumina) sequence data to a reference genome (`Alkan et al, <2011 http://www.nature.com/nrg/journal/v12/n5/full/nrg2958.html>`_). `Layer et al (2014) <https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-6-r84>`_ describe Lumpy, a program that detects structural variation in whole-genome sequencing data by synthesizing information from different kinds of read alignment results - split reads (where a single read aligns to two different locations), discordant read pairs (where the paired-end reads from a single fragment align to locations inconsistent with that expected based on the fragment sizes in the sequencing library), or differences in read depth (due perhaps to variation in copy number of a particular sequence in the sample genome relative to the reference).

+ Efficient analysis of data from population-level whole-genome sequencing projects in humans is essential, due to the size of the human genome and the computational intensity of sequence alignment and variant detection. `Johnston et al (2017) <http://www.pnas.org/content/114/10/E1923.full>`_ describe two new programs, PEMapper and PECaller, to improve the efficiency of these analyses. Another paper, `Smith et al (2017) <https://academic.oup.com/gigascience/article/6/10/1/4160384>`_, also describes a new program to identify sequence variants, although their program begins with BAM alignment files produced by a short-read aligner.

+ `Firtina & Alkan (2016) <https://academic.oup.com/bioinformatics/article/32/15/2243/1743552>`_ report that changing the order of sequence reads in a FASTQ file, followed by alignment of the reads to the human reference genome and SNP calling with various software tools shows discordance in identified variants, ranging from less than 1% to around 25%.

+ Variant normalization, or reconciling differences in alignments and SNP or indel calls in low-complexity regions, is an important topic for researchers interested in making a complete catalog of genetic variation in a population. A seminal paper by `Tan et al (2015) <https://www.ncbi.nlm.nih.gov/pubmed/25701572>`_ introduced software for variant normalization using a VCF file and the reference sequence.  `Bayat et al (2017) <https://www.ncbi.nlm.nih.gov/pubmed/27993787>`_ reported additional concerns regarding the normalization algorithm used by other software and offered another software package they believe does a better job.


Exercises
*********

1. Erik Garrison, lead author of the Freebayes SNP caller, has an `exercise in alignment and variant calling <https://github.com/ekg/alignment-and-variant-calling-tutorial>`_ on his Github page, using both E. coli and human datasets downloaded from web sources. The software required for this tutorial is installed in the VCL machine image. A set of `slides <https://drive.google.com/open?id=1XR3kHmCQrTMs007oFKyMs-Qo04lW30vU>`_ from a presentation Garrison gave in 2015 describing the Freebayes SNP caller and how it is used in the 1000 Genomes project exploring human genome diversity are also available.

|

2. Data from an exercise presented at a `2016 Canadian bioinformatics workshop <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/>`_ are in /data/Module3.tar.gz in the VCL machine image.

|

3. Web pages describe the steps required to `align samples <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/mapping>`_ of reads from normal and tumor samples to a reference human genome sequence, then analyze the resulting alignments to identify `rearrangements <http://bioinformatics-ca.github.io/bioinformatics_for_cancer_genomics_2016/rearrangement>`_. 

------------------
	
**IMPORTANT NOTES**

	The full human reference genome sequence is too large to work in the alignment step, so after you unpack the Module3.tar.gz archive, you will need to change into the Module3 directory and extract the reference sequences for chromosomes 3, 6, 9 and 12 (because those have rearrangements on them) to a new file. I used the command 
::

	bioawk -cfastx '{if($name==3 || $name==6 || $name==9 || $name==12) {print ">"$name"\n"$seq}}' human_g1k_v37.fasta | fold | gzip > chr36912.fa.gz

\	
			to do this extraction; other ways are possible as well. The process will take a few minutes, so don't assume that something is wrong if you don't get a terminal prompt back right away after entering this command.

			After extracting the subset of 4 chromomes from the complete reference genome, you will have to create a BWA index before aligning reads to the four chromosomes of interest. I used the command 

::

	bwa index -p subset chr36912.fa.gz

|

		to create an index with the name 'subset'. This will take 10 or 15 minutes, so don't be impatient.

|

------------------

4. Map the normal tissue-derived and tumor-derived reads back to the reference genome sequence, piping the SAM-format output from the BWA mem aligner to samtools sort to sort the BAM file by reference position so alignment viewers can efficiently display the resulting alignments. I used the following command line:

 ::

	bwa mem -t3 subset reads.tumour.fastq | samtools sort -o tumor.bam - 

|

	the alignment took about 6 minutes for the tumor-derived reads. Modify this command line to align the normal-tissue-derived reads to the same reference, convert the output to BAM, and sort the output BAM file. After both BAM files are complete, use the samtools index command to produce index files for each of them.

|

5. The command to produce files of discordant reads from the BAM alignments uses the "flag" column of SAM format, which is a numerical value that contains answers for 12 different yes-or-no questions. The `Explain SAM flags <https://broadinstitute.github.io/picard/explain-flags.html>`_ web page has a list of the 12 properties of reads that make up the flag value; if the value 1294 is entered in the box, the corresponding properties of the reads are identified. The samtools view -F1294 option means "do not show reads with flags containing any of these values", effectively excluding reads with the checked characteristics from the ouput.

|

6. The command to produce files of split reads uses a script called extractSplitReads_BwaMem in the scripts subdirectory of the Module3 directory - make sure you use the correct path when you try to execute this command, and pay attention to the permissions on the files in the scripts subdirectory. How can you change the permissions to allow execution of all those script files?

|

7. The LUMPY program is installed in the VCL machine image and the path to the executable program is in the search PATH variable, so you should be able to execute that program without concern about what path to use to the program. The paths to the input files, and the names of the input files, however, must match those present on your instance of the machine image.


Additional Resources
********************

+ Information on the Sequence Alignment and Mapping (SAM) format is available at a University of Michigan `wiki <http://genome.sph.umich.edu/wiki/SAM>`_, at `Dave’s Wiki <http://davetang.org/wiki/tiki-index.php?page=SAM>`_, and in the SAM format `specification <http://samtools.sourceforge.net/SAM1.pdf>`_. 

+ Quality control of alignment files is a valuable preliminary step before investing significant time and effort in analysis. A package called *indexcov* is available to efficiently summarize coverage of different genomic regions within a single sample, or uniformity of coverage across multiple samples, beginning with alignments in BAM or CRAM formats. See Indexcov: fast coverage quality control for whole-genome sequencing. `GigaScience 6:1-6, 2017 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5737511/>`_


+ Genomic rearrangements in Arabidopsis considered as quantitative traits. `Imprialou et al, Genetics 205:1425-1441  <http://www.genetics.org/content/205/4/1425>`_, 2017. *This paper describes a strategy for mapping likely locations of structural rearrangements in a segregating population of recombinant inbred lines using low-coverage (0.3x) whole-genome resequencing.*

+ LUMPY: a probabilistic framework for structural variant discovery. `Chiang et al, Genome Biology 15:R84, <https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-6-r84>`_ 2014.

+ CNVnator: An approach to discover, genotype, and characterize typical and atypical CNVs from family and population genome sequencing. Abyzov et al, `Genome Research 21: 974-984, <http://genome.cshlp.org/content/21/6/974.full>`_ 2011.

+ Canvas: versatile and scalable detection of copy number variants. Roller et al., `Bioinformatics  32: 2375-2377, <https://academic.oup.com/bioinformatics/article/32/15/2375/1743834/Canvas-versatile-and-scalable-detection-of-copy>`_ 2016.

+ Genome structural variation discovery and genotyping. Alkan et al, `Nature Reviews Genetics 12:363-376, <http://www.nature.com/nrg/journal/v12/n5/full/nrg2958.html>`_ 2011.




Last modified 27 December 2018.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
