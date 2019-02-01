.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


Transcriptome Assembly
======================

Global Overview
***************

Multiple options are available for reconstruction of the sequences of RNA transcripts based on analysis of complementary DNA copies, depending on whether a high-quality reference genome assembly is available. If so, reference-guided transcriptome assembly using a splice-aware sequencer aligner followed by resolution of alternative splicing variants and export of consensus transcript sequences can be powerful (`Trapnell et al., 2012 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3334321/>`_). If there is no reference genome assembly, or the available assembly is fragmented and poorly-annotated, a de-novo assembly of putative transcripts from short-read sequences is one alternative. The availability of long-read sequencing methods such as Oxford Nanopore Technologies and Pacific Biosciences has opened a third alternative, which is to obtain full-length sequences of cDNAs and report those sequences without the requirement for assembly at all (`Sharon et al., 2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4075632/>`_; `Bolisetty et al., 2015 <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-015-0777-z>`_; `Minoche et al., 2015 <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-015-0729-7>`_).

Objective
*********

The objective of this session is to introduce participants to methods for assembly of a transcriptome, or a collection of RNA transcripts present in a given RNA sample.  The RNA-seq data used in the differential gene analysis exercise will be used for this exercise as well, as those datasets are small enough to run on systems with only 8 Gb RAM.

Description
***********

De-novo assembly of short DNA sequence reads into contiguous full-length copies of RNA transcripts is a complex process, because there are multiple sources of variation in read coverage and in read sequences. Read coverage is proportional to transcript abundance, but can also be affected by biases due to library construction  methods and biological factors. A key factor leading to variation in transcript sequences, and therefore variation in read sequences, is alternative splicing of transcripts from the same transcription unit into different mature forms. Another factor affecting read sequences is the increased error rate of RNA polymerases relative to DNA polymerases - RNA sequences are inherently noisier than DNA sequences. Trinity (Grabherr et al, 2011) is a widely-used suite of programs for de-novo assembly of RNA-seq data; the `Rockhopper <https://cs.wellesley.edu/%7Ebtjaden/Rockhopper/>`_ program for assembly of bacterial RNA-seq data is described in a recent report (Tjaden, 2015). One key difference between these two programs is the amount of memory required - the recommended amount of RAM for Trinity is 1 Gb RAM per million reads in the dataset, while Rockhopper can carry out assembly of datasets with hundreds of millions of reads using 2 Gb of RAM.

Construction of a de Bruijn graph is one approach used to solve the computational problem of assembling short DNA sequence reads into accurate contigs that reflect the transcripts present in the original RNA sample used for library construction. A key difference between Trinity and Rockhopper in the amount of memory required is that Rockhopper builds an index of sequence contigs as they are assembled, so that the entire de Bruijn graph of all k-mers present in the full set of reads does not have to be held in memory for the entire process of assembly. `Slides <https://drive.google.com/open?id=118CkZLgeixZREUnd_UfvkJ2_ktrqhHty>`_ from `Lilian Matallana <https://www.linkedin.com/in/lilian-matallana-21704474/>`_'s lecture on de Bruijn graphs and their use in sequence assembly programs describe these different strategies in more detail.

Key Facts
*********

Paired-end sequencing reads are useful for assembly of eukaryotic transcriptomes, because the information they provide about the positions of sequences relative to each other within a transcript is valuable for correct assembly of alternatively-spliced transcripts. In bacteria, splicing is less frequent, alternative splicing can be less of a concern, and single-end reads can often be assembled into a reasonably accurate transcriptome. If alternative splicing is not of interest, then single-end reads are useful for RNA-seq analysis of eukaryotic transcriptomes as well - now that read-lengths of  100 to 150 nt are readily available, paired-end reads add little additional information regarding levels of gene expression.

\


Exercise - reference-guided assembly
************************************

Temporary direct download links for class can be found in the `Transcriptome_Assembly.txt <https://drive.google.com/open?id=1Xkr5_-k3lz6cNfiEOigiaKk8sj1Kdwm4>`_ file. 

+ The Arabidopsis thaliana RNA-seq dataset used for the analysis of differential gene expression includes six sequence files found in the `fullset.zip <https://drive.google.com/open?id=16W-W3t3DILI05cufENJRq8NnO1vz7mge>`_ archive in the `AtRNAseq <https://drive.google.com/open?id=1_-cX7Scvp_e8zlN4glcD3-i2eJg5Tv71>`_ archive.

\

+ The HiSat2 aligner is already installed on the VCL system. If you want to install it on another computer, an executable binary can be downloaded from the link under the Releases heading on the right side of the program `home page <http://ccb.jhu.edu/software/hisat2/index.shtml>`_. This program is the successor to Bowtie and Tophat, the original programs developed for reference-guided sequence assembly.

\

+ Create a folder for this exercise, and unpack the `Atchromo5.fasta.gz <https://drive.google.com/open?id=1i5p9JlQZh_xvhGN_d9JvLVaOxqF8Hp0_>`_ reference sequence from the /data/AtRNAseq folder into that directory. Use the hisat2-build program (from the hisat2-2.0.5 directory) to build an alignment index from the uncompressed fasta-format sequence data.

\

+ Unpack the three control-sample RNA-seq read files (named c1, c2 and c3) from the `fullset.zip <https://drive.google.com/open?id=16W-W3t3DILI05cufENJRq8NnO1vz7mge>`_ archive to a single fastq file, using the gzip -cd command with file globs.

\

+ Align the fastq-format sequence reads to the reference sequence using the hisat2 program (using the --dta option), and pipe the output to samtools1.3 view to convert the SAM output into BAM, then to samtools1.3 sort to sort the output BAM data and save it to a file.

\

+ Download the Linux x86_64 binary version of the StringTie program from the link under the Obtaining and installing StringTie heading on the program `home page <http://ccb.jhu.edu/software/stringtie/index.shtml>`_. Unpack the zip archive in your /home/lubuntu directory.

\

+ Execute the stringtie program using the sorted BAM file as input.

\


Exercise - de-novo assembly
***************************

+ The *Arabidopsis thaliana* RNA-seq dataset can also be used for de-novo assembly, although RAM is a limiting factor on instances of the VCL Biostar_DNASeq machine image.

\

+ `Rockhopper <https://cs.wellesley.edu/%7Ebtjaden/Rockhopper/>`_ can be downloaded to the home directory of a VCL instance and run from the command line  - for some reason the GUI version would not save the file of assembled transcripts when I tested it. All six files of RNA-seq data are from the same accession of Arabidopsis, so they can all be concatenated into a single file and provided as input to Rockhopper.

\

+ A file of *Arabidopsis thaliana* RNA sequences (inferred from gene models in the TAIR 10 genome assembly: `TAIR10.cDNA.fa.gz <https://drive.google.com/open?id=13n6Iu-Aht4ikGH2SyX0yTwKVfx3ply3R>`_) is also available. The assembled transcripts can be compared with these predicted transcripts as a means of evaluating how good a job the Rockhopper assembler (which is designed for assembly of bacterial RNA-seq datasets) does with the plant RNA-seq data.


\

Additional Resources
********************

Several papers have reported that the most reliable approach for transcriptome assembly for different organisms is to use multiple different programs for independent assemblies, followed by merging together of the resulting assembled contigs and selection of the most complete contigs as representatives for the final completed transcriptome. 
+ McManes, M.D. 2018 The Oyster River Protocol: a multi-assembler and kmer approach for de-novo transcriptome assembly. Peer J. 6:e5428. `Full text <https://dx.doi.org/10.7717%2Fpeerj.5428>`

\

+ Nakasugi et al, 2014 Combining transcriptome assemblies from multiple de novo assemblers in the allo-tetraploid plant Nicotiana benthamiana. PLoS ONE 9(3): e91776. `Full text <https://dx.doi.org/10.1371%2Fjournal.pone.0091776>`

\

Correction of errors in RNA-seq reads requires consideration of the difference in relative abundance among transcripts in order to identify likely error-derived k-mers. Rcorrector is one software package capable of this process.
+ Song & Florea, 2015. Rcorrector: efficient and accurate error correction for Illumina RNA-seq reads. Gigascience 4:48. `Full text <https://dx.doi.org/10.1186%2Fs13742-015-0089-y>`

\

+ One strategy for reducing the amount of RAM required for transcriptome assembly by the Trinity software package is to carry out "digital normalization" of the RNA-seq dataset - this means adjusting the numbers of reads in the dataset to ensure more uniform representation of both abundant and rare transcripts, while removing sequencing errors. A detailed `exercise <http://khmer-protocols.readthedocs.io/en/v0.8.4/mrnaseq/index.html>`_ is available, which uses AWS cloud computing instances to provide sufficient computing power to process a real dataset.

\

+ Analysis of Next Generation Sequencing data (ANGUS) is a workshop series on high-throughput sequence data analysis; the `2017 workshop <https://angus.readthedocs.io/en/2017/toc.html>`_ includes an `exercise <https://angus.readthedocs.io/en/2017/assembly-trinity.html>`_ on transcriptome assembly with Trinity using cloud computing resources.

\

+ Rana et al., 2016. Comparison of de-novo transcriptome assemblers and k-mer strategies using the killifish, Fundulus heteroclitus. PLoS One 11: e0153104. `Full text <http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0153104>`_

\

+ Boley et al., 2014. Genome-guided transcript assembly by integrative analysis of RNA sequence data. Nature Biotechnology 32: 341-346. `Publisher Website <http://www.nature.com/nbt/journal/v32/n4/full/nbt.2850.html>`_

\

+ Grabherr et al, 2011. Full-length transcriptome assembly from RNA-Seq data without a reference genome. Nature Biotechnology 29:644 - 652. `PubMed Central <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3571712/>`_

\

+ Tjaden, B. (2015) De novo genome assembly of bacterial transcriptomes from RNA-seq data. Genome Biology 16:1 `Full text <http://genomebiology.com/2015/16/1/1>`_

\

+ Gnerre S, et al. (2011) High-quality draft assemblies of mammalian genomes from massively parallel sequence data. Proc Natl Acad Sci USA 108:1513–1518. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3029755/>`_

\

+ Salzberg S, et al. (2012) GAGE: A critical evaluation of genome assemblies and assembly algorithms. Genome Research 22:557–567. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3290791>`_ This paper describes a set of experiments comparing different assembly programs on four genomes, and provides useful insights into the challenges of genome assembly.

\

+ Magoc T and Salzberg S. (2011) FLASH: Fast Length Adjustment of Short Reads to improve genome assemblies. Bioinformatics 27:2957–2963. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3198573/>`_ This paper describes a software tool for joining paired-end reads obtained from DNA fragments short enough that the reads overlap at the ends. This is reported to improve the quality of assemblies created from the joined reads. An outline of an exercise with the FLASH assembler is available: `FLASH_exercise.docx <p:%5Cfer%5CChristmas%20Tree%20Genetics%20Program%5COther%20Files%5CBIT815_WebpageCode%5CBIT815%5CDocuments%20for%20classes%5CWeek%204>`_

\

+ Pevzner PA, et al. (2001) An Eulerian path approach to DNA fragment assembly. PNAS 98:9748-9753. `Full Text <http://www.pnas.org/content/98/17/9748.full>`_


Last modified 31 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
