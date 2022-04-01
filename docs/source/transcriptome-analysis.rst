.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Transcriptome Analysis: Differential Gene Expression and Annotation
==================================================================



Global Overview
***************

Transcriptome analysis is a very broad topic that covers a spectrum from initial characterization of expressed genes in a non-model species with no other genomic information available, to detailed analysis of alternative splicing and gene expression among organs, tissues, or even individual cells of a model organism for which a well-annotated reference genome sequence is known. As previously noted, if the objective of a sequencing experiment is simply discovery of the sequence itself, then experimental design considerations may be less critical, but if the objective is to use the sequencing experiment as a quantitative measure of some biological process (such as gene expression or alternative splicing differences among individuals, developmental stages, or treatments), then an appropriate experimental design is essential.


Objective
*********

The objective of this session is to introduce participants to the additional complexity of analyzing transcriptomes by deep sequencing, above the already complex process of analyzing genome structure. RNA transcripts vary both in abundance, in primary sequence, and in the outcome of splicing processes. All these types of variation can have important biological effects, and may be of interest in a "transcriptomics" experiment. Annotation is the process of describing functional elements in genomes, including regions that are transcribed and processed into various kinds of functional RNA molecules. Messenger RNAs that encode proteins are an abundant class of functional RNA molecules, but by no means the only one - long non-coding RNAs, microRNAs, ribosomal RNAs and transfer RNAs are other important classes of functional RNA molecules. 



Description
***********

RNA-seq experiments are growing in popularity as a means of characterizing the transcriptome, detecting alternative splicing events, and measuring differences in gene expression between samples of different types. The importance of good experimental design in conducting RNA-seq experiments is emphasized in the first paper in the recommended reading, by Auer and Doerge. Any experiment in which differences between samples are to be interpreted in a biological context should take seriously the need for good experimental design. The most reliable conclusions will result from a well-replicated design in which the experimental treatments are orthogonal to nuisance factors. `Slides <https://drive.google.com/open?id=1NB2ICMSgcGO10v0i5ZhwQZuNhsMmR4C9>`_ with an overview of RNA-seq workflows and some discussion of experimental design and analysis strategies are available. Engström et al (`2013 <http://www.nature.com/nmeth/journal/v10/n12/full/nmeth.2722.html>`_) compared the performance of several different programs designed to align RNA-seq reads to reference genome sequences, and provide a thorough discussion of the advantages and disadvantages of the programs tested. More recently, Conesa et al (`2016 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4728800/>`_) surveyed best practices for RNA-seq experiments, and noted that no single workflow is optimal for every experiment. 

\

One exercise in RNA-seq data analysis will follow the description in the `EdgeR user's guide <https://bioconductor.org/packages/release/bioc/vignettes/edgeR/inst/doc/edgeRUsersGuide.pdf>`_ or the `DESeq2 vignette <https://bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html>`_ on your own or in class. The exercise is based on an experiment reported by Cumbie et al. (`2011 <http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0025279>`_), and involves comparison of gene expression levels in Arabidopsis plants inoculated with a bacterial pathogen or mock-inoculated with sterile solution. The complete data from the experiment are downloaded from `NCBI SRA <http://www.ncbi.nlm.nih.gov/sra/?term=SRP004047>`_ during the exercise using the `At_RNAseq.sh <https://drive.google.com/open?id=18NJkXMWjOLUzgiiez4Q-t_z6alM40h7Z>`_ script saved in the `AtRNAseq <https://drive.google.com/open?id=1_-cX7Scvp_e8zlN4glcD3-i2eJg5Tv71>`_ archive; R scripts to run differential gene expression analysis with **DESeq2** or **edgeR** packages are in the same directory. 


Key Facts
*********

RNA-Seq library construction strategies may be different for different experimental objectives:

+ Differential gene expression: one sequenced “tag region” per gene is enough to estimate relative levels of gene expression if a reference genome sequence is available to allow mapping tags uniquely to genes, but "tag sequencing" does not give information on alternate splicing.

\

+ Gene discovery: comprehensive coverage of transcripts is an asset to obtain complete sequences of expressed genes in species for which a reference genome sequence is not available. Normalization methods that reduce the difference in abundance among transcripts can work well to obtain more complete coverage of all transcripts, but may be a problem if accurate estimates of the relative abundance of transcripts is an experimental objective. Paired-end sequencing is useful for transcriptome assembly, because it provides more information about alternative splicing events and transcript structure for the assembly process.

\

+ Alternative splicing analysis: complete coverage of exons is essential, and estimates of relative abundance are important also. Long-read sequencing methods (PacBio and Oxford Nanopore) are becoming the method of choice for analysis of alternative splicing events because they allow analysis of combinations of alternative splicing events across the entire length of the mature transcript. This advantage is most important in studies of genes in which multiple sites of alternative splicing are known, and a central question of interest is which events occur in the same transcript.

Often researchers are interested in all aspects of transcriptome analysis – discovering new transcripts or alternate splicing events of annotated genes, plus measuring relative abundance and detecting genetic variation – so many RNA-Seq experiments use non-normalized libraries of cDNA synthesized by priming with random oligos, to give relatively uniform coverage across entire transcripts. Accurate reconstruction of alternatively-spliced transcripts from individual genes is an important part of RNA-seq data analysis if the experimental objectives include testing for significant differences in levels of alternatively-spliced transcripts among individuals (genetic variation in splicing) or among treatment groups (which may include developmental stages as well as environmental conditions or chemical exposures). Software designed to test for association between genetic variants and levels of alternatively-spliced transcripts is available (Monlong et al, `2014 <http://www.nature.com/ncomms/2014/140820/ncomms5698/full/ncomms5698.html>`_). Pipeline tools that combine multiple software packages into an integrated analytical approach have been described by multiple groups (Cumbie et al, `2011 <http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0025279>`_ and Varet et al., `2015 <http://biorxiv.org/content/early/2015/09/26/021741>`_ are examples); these may be worth setting up if you have a lot of data to analyze and want the added functionality of an integrated pipeline.

One disadvantage of using an integrated pipeline can be that the details of individual steps in the analysis are obscured, unless the end user can actually read the code and understand what each step of the pipeline does. This can make it difficult to know exactly what analytical routines are used, or how appropriate they are to the user's dataset. This can be especially important in dealing with sources of bias, such as transcript length and GC content, that can affect the results of differential expression analysis from RNA-seq experiments. Mandelboum et al (`PLoS Biol 17:e3000481, 2019 <https://doi.org/10.1371/journal.pbio.3000481>`_) reported that sample-specific variation in length effects resulted in biased results in 35 different datasets downloaded from the GEO database at NCBI, detected as a rank correlation between the log-fold change in expression of a transcript and the length of the transcript, even when comparing replicate samples of the same experimental treatment. Many current protocols for differential gene expression analysis include normalization for transcript length, but testing for a relationship between log-fold change in expression and transcript characteristics is a good control to test for possible bias. Hansen et al (`Biostatistics 13:204, 2012 <https://doi.org/10.1093/biostatistics/kxr054>`_) described conditional quantile normalization to reduce bias due to GC content or transcript length, and this method was reported by Mandelboum et al to mitigate the bias they observed in the published datasets they analyzed.


Exercises
*********

You can use the commands found in the `Transcriptome_data.txt <https://drive.google.com/open?id=1jSNUzeBRg1dExWJhI2ylxRfggHYh4s1->`_ to download the required archives directly from the command line. 

1. The experimental data from `Cumbie et al 2011 <http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0025279>`_ is saved in the `AtRNAseq <https://drive.google.com/open?id=1_-cX7Scvp_e8zlN4glcD3-i2eJg5Tv71>`_ archive. The files `c1.fq.gz <https://drive.google.com/open?id=1A1ePOEEQxgY5-WbtH99_-wfpivYpLRyT>`_, `c2.fq.gz <https://drive.google.com/open?id=1OIwpkuNJIAhfDoXFsfAiEbCho6EXt412>`_, and `c3.fq.gz <https://drive.google.com/open?id=1DhVkPmszlpvH8dIKXef2iiSO-cF_cj-v>`_ contain sequence reads from three biological replicates of control samples, and files `t1.fq.gz <https://drive.google.com/open?id=13xP7gcbNCT8BwbGh1_bLg6LF_AWfruhn>`_, `t2.fq.gz <https://drive.google.com/open?id=1_gPRcV7zzs8HixgK7dwNRb-h8MPXjMpc>`_ and `t3.fq.gz <https://drive.google.com/open?id=1wr0qCiomXFSiB2T9zdrzYRSB7FcW67Cy>`_ contain sequence reads from three biological replicates of test samples. The file `Atchromo5.fasta.gz <https://drive.google.com/open?id=1i5p9JlQZh_xvhGN_d9JvLVaOxqF8Hp0_>`_ contains the sequence of Arabidopsis chromosome 5, and the file `TAIR10.cDNA.fa.gz <https://drive.google.com/open?id=13n6Iu-Aht4ikGH2SyX0yTwKVfx3ply3R>`_ contains predicted transcripts from the TAIR10 Arabidopsis genome assembly. Matrices produced by Salmon using k-mer-based "quasi-mapping" of `read counts <https://drive.google.com/a/ncsu.edu/file/d/1E37JMBl76XPvVlfGKGIha5PPL1Ow8EqF>`_ or `read TPM values <https://drive.google.com/a/ncsu.edu/file/d/1fyhuRyJmh6f0j5ktEUHveoIsg_k1W6OV>`_ are available; these can be imported into DESeq2 or edgeR sessions and analyzed according to the vignettes for those packages (links provided above or with `direct download text <https://drive.google.com/open?id=18U7valM4P4r2topHWkRsqDzC_I9RtXn3>`_). 

\
 
2. A script to download the complete data from the Sequence Read Archive at NCBI is `At_RNAseq.sh <https://drive.google.com/open?id=18NJkXMWjOLUzgiiez4Q-t_z6alM40h7Z>`_, and scripts to analyze the resulting data with `kallisto <https://drive.google.com/open?id=1EbVcHki5CeE2CGYGc682XFl4lQjKBbsB>`_ and either `edgeR <https://drive.google.com/open?id=1T_Am4Aj_RnYw-kFWpJFetNXo-DXNS_h1>`_ and `DESeq2 <https://drive.google.com/open?id=1fXbjVEqA-YRb_Vwd3C2MH17aBct6Tp5N>`_ are also available - these scripts are saved in the AtRNAseq archive from the google team drive, and links are provided here for those who want to try the analysis on other machines. A script to load output from `RSEM into R <https://drive.google.com/open?id=18q0rowXeDdbJC1D6agIg9cIptB9VDHsT>`_ for analysis  is also available.

\
 
3. A fairly comprehensive discussion of RNA-seq workflow options (including different approaches to producing tables of read counts from BAM alignment files) is available in a `Bioconductor tutorial on gene-level exploratory data analysis <http://www.bioconductor.org/help/workflows/rnaseqGene/>`_; a description of using biomaRt, GO, and KEGG for annotation is given in `this tutorial <https://cran.r-project.org/web/packages/biomartr/vignettes/Functional_Annotation.html>`_. 

\
 
4. Another good overview of RNA-seq analysis is `RNAseq Analysis in R <https://combine-australia.github.io/RNAseq-R/>`_, which contains materials (both lecture slides and hands-on computing exercises) for a multi-day workshop. The materials include visualization using heat maps, volcano plots, clustering, and a variety of other methods, using example data from mouse to take advantage of the available annotation to do gene set enrichment analysis.
 

\

5. The "Tuxedo" package of programs (`Bowtie2 <http://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.0/bowtie2-2.3.0-linux-x86_64.zip>`_, `Tophat <http://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz>`_, `Cufflinks <http://cole-trapnell-lab.github.io/cufflinks/assets/downloads/cufflinks-2.2.1.Linux_x86_64.tar.gz>`_) provide splice-aware read alignment, transcript reconstruction, and estimation of transcript abundance. The latest versions of Bowtie2, Tophat, and Cufflinks are available as compiled executables, and those version can read and write gzipped files. Simply download and unpack the archives for each program, then create a symbolic link between the program and the /usr/local/bin directory

\
 
6. A complete tutorial for analysis of RNA-seq data using Tophat and Cufflinks is available in `Trapnell et al (2012) <http://www.nature.com/nprot/journal/v7/n3/full/nprot.2012.016.html>`_; this can be used as a guide to carry out analysis of the control and test datasets used for the RNA-seq exercise described above.

\

7. An older `tutorial <http://girke.bioinformatics.ucr.edu/CSHL_RNAseq/mydoc/mydoc_systemPipeRNAseq_02/>`_ for Gene Ontology (GO) Term Enrichment from RNAseq analysis. The tutorial from a Cold Spring Harbor Plant Biology short corse contains information on the overview of the GO term enrichment and notes on the sampling procedure used to shrink the dataset from the `full NCBI record <https://www.ncbi.nlm.nih.gov/bioproject/PRJNA156671>`_. For more information the `Gene Ontology page <http://geneontology.org/docs/go-annotations/>`_ has links to the annotation tables of various organisms. Additionally, a `vignette for the goseq package <https://bioconductor.org/packages/3.4/bioc/vignettes/goseq/inst/doc/goseq.pdf>`_ for GO Term Enrichment using v3.4 of Bioconductor is also available. 

\

8. An exercise in evaluating the influence of total read depth on the sensitivity and precision of detecting genes using RNA-seq data is available. The `download.bamfiles.sh <https://drive.google.com/a/ncsu.edu/file/d/1ZGfoQ9v6x1gIrt9JdxrgGyewG0GB4bZ8>`_ script will download a set of BAM files from Google Drive and run the Hisat2 reference-guided transcript assembler on the files, then compare the GTF files output from the Hisat2 runs with the TAIR10 Arabidopsis reference genome assembly annotation to assess the sensitivity and precision of detecting annotated genes from RNA-seq data. These data are from the study of `Marquez et al, 2012 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3371709/>`_ - the BAM files contain only reads aligning to chromosome 2 of the Arabidopsis genome, and were subsampled to represent 20%, 40%, 60%, and 80% of all the available data, as well as the complete set of reads aligned to chr2. A set of `questions <https://drive.google.com/a/ncsu.edu/file/d/1sP1sULzovd1E6LzeDEi0_8Aq1fqrCe-8>`_ to answer about the output from the experiment is also available. Important sources of information include the `Stringtie manual <http://ccb.jhu.edu/software/stringtie/index.shtml?t=manual>`_ and the `GFFcompare manual <https://ccb.jhu.edu/software/stringtie/gffcompare.shtml>`_ webpages.

\

9. An exercise on annotation of assembled transcripts (either reference-guided or de-novo assembled) with TransDecoder is available. The `annotation.sh <https://drive.google.com/a/ncsu.edu/file/d/1CdT4XDvtTAqWn9R1w6UoGsQ9mlFssGj_>`_ script file picks up where Exercise 8 ends, and assumes that the GTF file produced by Stringtie reference-guided assembly of RNA-seq reads is available. Some editing of the script will be necessary to make sure the file names and paths are correct for the files you are using for the annotation exercise. The text file `Trinotate_Bioconda_install.txt <https://drive.google.com/a/ncsu.edu/file/d/1vcVevB4jaBWUarIM7rWMo_ELFphKSd2Y>`_ has information on how to install the complete Trinotate annotation pipeline using Bioconda - this may work on the VCL image, but will be most useful on the HPC because it has more resources available to actually process large datasets.

Additional Resources
********************

+ `Statistical design and analysis of RNA sequencing data <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2881125>`_. Auer & Doerge, Genetics 185(2):405-416, 2010.

\

+ `Recurrent functional misinterpretation of RNA-seq data caused by sample-specific gene length bias <https://doi.org/10.1371/journal.pbio.3000481>`_. Mandelboum et al, PLoS Biol 17: e3000481, 2019. *Transcript length is correlated with log-fold change in expression levels in 35 published RNA-seq datasets after normalization with five different methods, according to these authors. They recommend conditional quantile normalization as a way to reduce the bias due to differences in transcript length and GC content.*

\

+ BAM alignment files are not the only way to estimate the number of transcripts from each gene detected in an RNA-seq dataset; an alternative approach is to create a k-mer hash table of the transcripts that might be detected, then use that table to analyze the filtered and trimmed reads themselves to estimate the count of reads from each transcript, and therefore the counts for each transcript detected. Software tools to carry out this type of transcript-count estimation include `Sailfish <http://www.cs.cmu.edu/~ckingsf/software/sailfish/>`_,  `Salmon <https://combine-lab.github.io/salmon/>`_, `Kallisto <https://pachterlab.github.io/kallisto/about>`_, and `HTSeq <http://www-huber.embl.de/HTSeq/doc/overview.html>`_.

\

+ `DE-kupl: exhaustive capture of biological variation in RNA-seq data through k-mer decomposition <https://doi.org/10.1186/s13059-017-1372-2>`_ Audoux et al, Genome Biol 18:243, 2017. *These authors developed the DE-kupl software tool for reference-free transcriptome analysis using kmer decomposition of RNA-seq sequencing reads. This can be a powerful tool for analysis of organisms with no previous genomic information, or for detection of novel events in species (such as human) with well-annotated genome and transcriptome data.*

\ 

+ `Ultrafast functional profiling of RNA-seq data for nonmodel organisms <https://doi.org/10.1101/gr.269894.120>`_  Liu et al, Genome Research  31: 713-720, 2021 *These authors developed another reference-free kmer-based analysis tool for RNA-seq data, called* `Seq2Fun <https://www.seq2fun.ca/>`_. *The Seq2Fun pipeline translates RNA-seq reads into all six reading frames and searches databases of peptide sequences to identify homologous proteins, and produces output including transcript abundance tables, biochemical pathway information, and species of origin. The output from Seq2Fun can be used as input to* `NetworkAnalyst <https://www.networkanalyst.ca/>`_ *to carry out Gene Ontology (GO) and KEGG annotation and pathway analysis.*

\

+ `Choice of library size normalization and statistical methods for differential gene expression analysis in balanced two-group comparisons for RNA-seq studies <https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-020-6502-7>`_. Li et al, BMC Genomics 21:75, 2020.  *These authors compare different normalization methods and statistical tests for sensitivity and specificity in analysis of simulated RNA-seq datasets, where the correct answer is known, and report that different methods give optimal results depending on the experimental design.*

\

+ `CHESS: a new human gene catalog curated from thousands of large-scale RNA sequencing experiments reveals extensive transcriptional noise. <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1590-2>`_ Pertea et al, Genome Biol 19:208, 2018. *These authors report the discovery of 224 novel protein-coding genes and 116,156 novel transcripts in the human genome, in additional to millons of transcripts they hypothesize are transcriptional 'noise'. See also the* `Research Highlight <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1600-4>`_ *by W.F. Doolittle in the same issue of the journal, which discusses the definition of gene function as "honed by natural selection in order to contribute to organismal fitness", and the alternative perspective that suggests that transcribed regions of the genome must have a function because they are transcribed.*

\

+ `Protocol update for large-scale genome and gene function analysis with the PANTHER classification system (v.14.0) <https://doi.org/10.1038/s41596-019-0128-8>`_ Mi, et al.Nat Protoc 14, 703–721 (2019). *PANTHER is a database of gene orthologues with Gene Ontology classication and assignments to biochemical pathways, searchable by several methods to allow researchers to recover annotation information important for providing biological context to the results of transcriptome analysis experiments.*

\

+ `Systematic and integrative analysis of large gene lists using DAVID bioinformatics resources. <https://www.nature.com/nprot/journal/v4/n1/pdf/nprot.2008.211.pdf>`_ Huang et al, Nature Protocols 4: 44-57, 2009

\

+ `Identification of genetic variants associated with alternative splicing using sQTLseekeR. <http://www.nature.com/ncomms/2014/140820/ncomms5698/full/ncomms5698.html>`_ Monlong et al, Nature Comm 5:4698, 2014 

\

+ `Scotty: a web tool for designing RNA-Seq experiments to measure differential gene expression. <http://bioinformatics.oxfordjournals.org/content/29/5/656>`_ Busby et al, Bioinformatics 29:656–657, 2013 

\

+ `Systematic evaluation of spliced alignment programs for RNA-seq data. <http://www.nature.com/nmeth/journal/v10/n12/full/nmeth.2722.html>`_ Engström et al, Nature Methods 10:1185-1191, 2013. *This paper reports results of comparisons of several different splice-aware alignment programs, and concludes that none of the programs tested is optimal by all criteria. The STAR alignment program (Dobin et al, 2013; see next reference) ranks highly by most measures, though, and is recommended for use by the Broad Institute as part of their* `Best Practices <https://www.broadinstitute.org/gatk/guide/best-practices?bpm=RNAseq>`_ *pipeline for variant discovery in RNA-Seq experiments.*

\

+ `STAR: ultrafast universal RNA-seq aligner. <http://bioinformatics.oxfordjournals.org/content/29/1/15>`_ Dobin et al, Bioinformatics 29:15-21, 2013

\

+ `A survey of best practices for RNA-seq data analysis. <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4728800/>`_ Conesa et al, Genome Biology 17:13, 2016 

\

+ `GENE-counter: a computational pipeline for the analysis of RNA-seq data for gene expression differences. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0025279>`_ Cumbie et al, PLoS ONE 6(10): e25279, 2011.

\

+ `Molecular indexing enables quantitative targeted RNA sequencing and reveals poor efficiencies in standard library preparations. <http://www.pnas.org/content/111/5/1891>`_ Fu et al, PNAS 111:1891–1896, 2014

\

+ `Robust adjustment of sequence tag abundance. <http://www.ncbi.nlm.nih.gov/pubmed/24108185>`_ Baumann & Doerge, Bioinformatics 30(5):601-605, 2014

\

+ `Differential analysis of gene regulation at transcript resolution with RNA-seq. <http://www.nature.com/nbt/journal/v31/n1/full/nbt.2450.html>`_ Trapnell et al, Nat Biotechnol 31:46-53, 2013

\

+ `Improving RNA-Seq expression estimates by correcting for fragment bias. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3129672/>`_ Roberts et al, Genome Biol 12:R22, 2011


Class Recordings
----------------

+   `Session 20: recorded March 10th 2021 <https://drive.google.com/file/d/1_0E405_-u_ulhbgwlV-khTmSDKMnsdQZ/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1PJqv2sx8YO3cEGwzIY1CD3WlU9YXB7G_/view?usp=sharing>`_.

+   `Session 21: recorded March 12th 2021 <https://drive.google.com/file/d/1JQK8p4CFNxl5zxP1WGu8awQMuw02bHy7/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1chh1eoUdhSXkDmTWu2aQptxRwC4shYMt/view?usp=sharing>`_.

+   `Session 22: recorded March 15th 2021 <https://drive.google.com/file/d/1elLZ8Z7MXQJE6pK8NUWdMoFZDwap7_W5/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1IpR7H-N-hr_p9FrXNiIkzRCS42WtQwtZ/view?usp=sharing>`_.

+   `Session 23: recorded March 17th 2021 <https://drive.google.com/file/d/17UQQzuNQXJfQ7miwJ5_BZbkCCqloJLgq/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1WvrWkxjiRpeusg_-50t23alBx7WsuK_O/view?usp=sharing>`_.

+   `Session 24: recorded March 19th 2021 <https://drive.google.com/file/d/1TKlDlcxupa-qZGopSGF8gVIkVZgtbtwV/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1JgJ7LpdjXQmOQFFIfuAhOjYOq4I5ajiR/view?usp=sharing>`_.


Last modified 31 March 2022.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
