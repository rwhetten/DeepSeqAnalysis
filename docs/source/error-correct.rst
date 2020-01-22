.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Error Correction and Alignment
==============================

Global Overview
***************

Sequences randomly sampled from genomic DNA can be assumed to be drawn from a uniform distribution across all possible sequences in the genome, although this assumption is typically violated at least to some degree, even with PCR-free libraries (`Kozarewa et al, 2009 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2664327/>`_). Based on that assumption, however, it is possible to analyze the distribution of frequencies of k-mers (short oligonucleotides, typically in the range from 15 to 31 bases) observed in sequence reads. If the average coverage of the genome is 50x, one expects to see most k-mers drawn from single-copy sequences in the genome around 50 times, with a sampling distribution that extends above and below that expected value. Errors in sequencing reads give rise to novel k-mers that typically appear much less frequently than the correct k-mer sequences, while k-mers drawn from sequences that are repeated in the genome (such as transposable elements) appear much more frequently than the single-copy k-mers. These differences can be used to filter out error k-mers and selectively remove reads containing sequencing errors from the dataset. The number of different k-mers detected, and the characteristics of the frequency distribution of kmers, can be used to estimate the size of the genome and the content of repetitive DNA sequences (`Li and Waterman, 2003 <http://genome.cshlp.org/content/13/8/1916.full>`_).

The underlying assumption that all k-mers are sampled from a uniform distribution is grossly violated in RNA-seq data and some other data types, so k-mer counting for purposes of error correction requires modeling the frequency distributions of kmers independently for transcripts of different abundance classes (`Song and Florea, 2015 <https://gigascience.biomedcentral.com/articles/10.1186/s13742-015-0089-y>`_). More sophisticated models can take base quality scores or k-mer abundance values into account, along with the connectivity of k-mers in the De Bruijn graph used for assembly (`Durai and Schulz, 2019 <https://www.nature.com/articles/s41598-019-41502-9>`_), and can combine normalization (reducing the computational load for transcriptome assembly) with error correction.  


Objective
*********

The objective of this session is to introduce concepts behind error correction algorithms, and to provide participants experience in simulating short-read sequence data, using error-correction programs, and aligning short read sequence data to a reference genome. The resulting alignment files will be compared to determine the effects of different error models during simulation, the value of error correction, and the outcomes of different alignment programs.


Description
***********

Ultra-high-throughput DNA sequencing platforms typically have much higher error rates than Sanger sequencing, and the sequence variation introduced by sequencing errors must be taken into consideration in downstream analysis of the DNA sequence data. Various approaches to error correction are possible, but each has disadvantages - some are too computationally-intensive for application to anything larger than a microbial genome, some make unjustified assumptions about the distribution of read coverage across the sequenced DNA template, and some lack sensitivity or specificity to resolve sequencing errors from true variants. Empirical datasets can be used to create statistical models of sequencing errors, and those error models can then be used to simulate sequencing data from a reference sequence for use in comparative analysis, so the results can be compared back to the starting genome to determine how well the error correction algorithm worked. It has been noted (`Heydari et al, 2017 <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-017-1784-8>`_) that the true test of how well error correction works is the quality of the resulting assembly, rather than the difference in the number of mismatches noted after alignment of uncorrected or corrected reads to an existing assembly, but this is a much more time-consuming test of error-correction methods. The same authors developed an error correction program aimed at improving the outcome of genome assembly by focusing specifically on read pairs near regions of repetitive sequence, and report improved assemblies for six eukaryotic genomes relative to those obtained from uncorrected reads (`Heydari et al, 2019 <https://bmcbioinformatics.biomedcentral.com/track/pdf/10.1186/s12859-019-2906-2>`_).


Key Facts
*********

Simulation is an important tool for development of new software and comparison of available software tools for specific purposes. The assumptions made in creating simulated datasets often determine the relative performance of different analytical approaches, so it is important to know what assumptions are made during simulation and how realistic those assumptions are for real datasets. In the exercises below,  simulated Illumina paired-end reads created from a reference bacterial genome (*Lactobacillus helveticus* strain `DPC4571<https://drive.google.com/open?id=1N_8e4SAj4SU_Y0zoYzA8_s3k1vXZCMtd>`_) are used.  The simulated read files (`sim.r1.fq.gz <https://drive.google.com/open?id=129qylzArUm3-K6-Rv8ORKqBwURuzwu5m>`_ and `sim.r2.fq.gz <https://drive.google.com/open?id=1ETW5KbnT7MTmxznzJSaUrTEKkhZmb-7A>`_) and the reference bacterial genome file are provided in the `DPC_4571 <https://drive.google.com/open?id=1PWLCABfrEpxAeG0XOBwPsDBE_KxBqG3N>`_ archive. GemReads.py (a Python script from the `GemSIM <http://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-13-74>`_ package) was used to create the simulated Illumina reads, and this package is installed in the VCL system, so you can create your own simulated datasets from the reference genome, but this is too time-consuming to do in class. GemReads.py does not accept gzipped files as input, so you will have to unpack the compressed genome sequence file.

It is important to note that while we use simulation as a tool, it is not the primary focus of the exercise. Instead, the focus of the exercise is on the use of error correction software, and what the effects of using error-correction software may be on the outcome of the overall experiment.

Exercises
*********

The text file `error_correction_files.txt <https://drive.google.com/open?id=1doOQv2I4gKxNJspk88XmgiGAOQc53b7E>`_ contains a list of commands for the direct download of files necessary for the following exercises. These commands are given for the benefit of those who use an SSH connection to a compute node or virtual machine instance, and don't have a web-browser interface available from which to download the datafiles to the instance. For users who have access to a virtual instance with a graphic interface, starting a web browser and downloading each file directly from the link is probably easiest.

\

1. The first exercise will align RNA-seq reads to a bacterial genome, to provide some experience with alignment software and an opportunity to explore software tools used to summarize and manipulate Sequence Alignment and Mapping (SAM) format files. The `RNA-seq reads<https://drive.google.com/a/ncsu.edu/file/d/1Vo90SPDoe9s-NDuwATPNLwRkBE6Q-Ny3>`_ come from *Lactobacillus helveticus* strain CNRZ32, while the reference genome is from strain `DPC 4571<https://drive.google.com/open?id=1N_8e4SAj4SU_Y0zoYzA8_s3k1vXZCMtd>`_, so some sequence differences detected in the alignments will be due to the strain divergence, and some differences due to sequencing errors or other sources of experimental noise in the RNA-seq data. You can also download a `text file<https://drive.google.com/a/ncsu.edu/file/d/1f_SkLZ0yqfjKQibUITKgpC1czd0x9_Df>`_ of steps to use in aligning the reads to the reference genome, then reviewing the results of the alignment. 

\

2. The MaSuRCA (Maryland SuperRead - Celera Assembler) program is installed on the VCL machine image. This program uses k-mers detected in filtered and trimmed fastq sequence reads to expand typical paired-end reads from an Illumina sequencing instrument into what it calls "super-reads". 

Download the `K-merCounting_ErrorCorrection.sh <https://drive.google.com/open?id=10sE787NiHKaoB1-vKhXbdHwYtlmRe-vh>`_ shell script, open it with the Geany or SciTE text editor (in the Applications menu under Development),  and review the commands and comments in the script file. These commands show how to use a simulation program called GemReads.py to simulate short sequence reads from the reference bacterial genome sequence. Type GemReads.py -h at a terminal prompt to get a list of options used to specify parameters of the simulation. The reference bacterial genome is 2.1 Mb - how many paired-end 100-nt Illumina reads would be required to reach average nucleotide coverage of 50x? What nucleotide coverage would be provided by 300,000 pairs of 100-nt reads?

\

3. The MaSuRCA installation also installed the Jellyfish k-mer counting program, and the Quorum error correction program as part of the MaSuRCA package. Use the Jellyfish k-mer counting program to produce a file with frequency data kmers of length 20, as outlined in the `K-merCounting_ErrorCorrection.sh <https://drive.google.com/open?id=10sE787NiHKaoB1-vKhXbdHwYtlmRe-vh>`_ script, then use the `plot_histo.R <https://drive.google.com/open?id=1aQIbTzaBYcbZretJg755lkeCGEwGjamm>`_ script to produce a PNG image file with a plot of the frequency distribution.

\

4. Use the Quorum error correction program to correct errors in the simulated sequence data. Type the full path to the /usr/local/masurca/bin/quorum program, followed by the -h option, at a terminal prompt to get help on the correct syntax to use the program. Run Quorum to correct the sequence reads, and save the corrected reads to new files.

\

5. Use the `BWA <http://bio-bwa.sourceforge.net/bwa.shtml>`_ or `Bowtie2 <http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml>`_ alignment programs to align the uncorrected and corrected sequence reads to the reference genome. Manuals for these two programs are available on Sourceforge - follow the links on the program names - and both programs are already installed on the VCL system.

\

6. Summarize the resulting SAM output files using the command-line tools grep, awk, cut, sort, and uniq, as described in `SAMformatAndCLtools.pdf <https://drive.google.com/open?id=1fA8Lam8lYaAM6venR3x6_rXO0MGPqO2O>`_

\

7. For extra practice working with SAM alignment files, download the `smallfiles.zip <https://drive.google.com/open?id=1K2ubY5OkY-JiA_hcdJSambb03pQyyq9C>`_ archive into your working directory and unpack the archive with the command :code:`unzip smallfiles.zip` Use the command-line tools grep, awk, cut, sort, and uniq, as described in the `SAMformatAndCLtools.pdf <https://drive.google.com/open?id=1fA8Lam8lYaAM6venR3x6_rXO0MGPqO2O>`_ document, to analyze the smallRNA-seq.sam file of read alignments. The same types of analyses can be carried out on the `sampleReadsSAM.tgz <https://drive.google.com/open?id=1zhNSU1j2Kr5Ptyjuv3-KY5gJzPw0MZeh>`_ file.


Additional Resources
********************

+ Song L, Florea L (2015) Rcorrector: efficient and accurate error correction for Illumina RNA-seq reads. GigaScience 4:48 `Full Text  <https://gigascience.biomedcentral.com/articles/10.1186/s13742-015-0089-y>`_

\

+ McElroy KE, Luciani F, Thomas T. (2012) GemSIM: general, error-model based simulator of next-generation sequencing data. BMC Genomics 13: 74. `PMID 22336055 <http://www.ncbi.nlm.nih.gov/pubmed/22336055>`_ *(Note: This paper describes software for simulation of sequence data that is useful for testing effects of error frequency on alignment and assembly).*

\

+ Marçais G, Yorke JA, Zimin A. (2013) Quorum: an error corrector for Illumina reads. Preprint on arXiv.org, `arXiv:1307:3515 <http://arxiv.org/abs/1307.3515>`_

\

+ Li H (2015) BFC: Correcting Illumina sequencing errors. Bioinformatics 31:2885. `Publisher Website <https://academic.oup.com/bioinformatics/article/31/17/2885/183855>`_

\

+ Li H, Durbin R. 2010 Fast and accurate long-read alignment with Burrows-Wheeler transform. Bioinformatics 26(5):589-95. `PMID 20080505 <http://www.ncbi.nlm.nih.gov/pubmed/20080505>`_ *(The original publication describing the BWA alignment program)*

\

+ Li H, Handsaker B, Wysoker A, Fennell T, Ruan J, Homer N, Marth G, Abecasis G, Durbin R; 1000 Genome Project Data Processing Subgroup. 2009. The Sequence Alignment/Map format and SAMtools. Bioinformatics 25(16):2078-9. `PMID 19505943 <http://www.ncbi.nlm.nih.gov/pubmed/19505943>`_ *(The original publication describing SAM format and SAMtools software)*

\

+ Hatem A, Bozdag D, Toland AE, Çatalyürek ÜV. 2013. Benchmarking short sequence mapping tools. BMC Bioinformatics 14:184. `PMID 23758764 <http://www.ncbi.nlm.nih.gov/pubmed/23758764>`_ *(A  publication comparing eight different open-source or proprietary read-alignment programs on simulated and real data, including BWA and Bowtie2. The conclusion was that no single tool is optimal for every purpose or any dataset; the user must make an informed decision based on experimental system and objectives)*



Last modified 22 January 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
