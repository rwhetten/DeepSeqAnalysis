.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Genome or Chromatin Structural Analysis: Chromatin immunoprecipitation, DNAse hypersensitivity, 3-D conformation
================================================================================================================



Global Overview
***************

High-throughput sequencing has been widely adopted as a method of collecting data about events that occur in genomes.  Examples of  events that occur in genomes include three-dimensional folding to pack genomic DNA efficiently into compact spaces, DNA modifications such as methylation or glycosylation, and interactions between DNA and regulatory or structural proteins. A reference genome sequence assembly is required for analysis of these types of genomic events, because the key question is one of quantitative differences among genomic locations - which sites in the genome show higher frequencies of events, and which show lower frequencies? This emphasis on quantitative analysis of the results means that experimental design is a critical part of this type of experiment. The goal should be to avoid confounding technical sources of variation (lane-to-lane variation on the sequencer, sample-to-sample variation in library preparation, etc) with biological variation of interest (differences between genotypes, treatment groups, developmental stages, or other biological factors).

\

A variety of specific file formats have been created for storage of data related to genomic location of different types of events. The University of California at Santa Cruz genome browser site includes a `FAQ list <https://genome.ucsc.edu/FAQ/FAQformat.html>`_ that describes many of these specialized file formats. Binary Alignment and Mapping (BAM), Browser Extensible Data (BED), General Feature Format (GFF), and Variant Call Format (VCF) are widely-used formats; some of the other formats described at the UCSC site are used primarily by human genome researchers.


Objective
*********

The objective of this session is to introduce methods for analysis of genomic events, using high-throughput sequencing primarily as a means of detecting specific fragments of DNA from a known reference genome. The DNA sequence itself is not the primary goal of the experiment in this case; it is simply a means of identifying specific regions of the genome that meet specific experimental criteria. These criteria can include


+	covalent modification of the DNA itself, such as methylation or other modifications of nucleotide residues in DNA, or covalent modification of DNA binding proteins such as methylation or acetylation of histones

\

+	modification of the arrangement of nucleosomes along the DNA or the physical packing of the DNA-histone complexes into higher-order chromatin

\

+	interactions between specific DNA regions and DNA-binding proteins such as transcriptional activators or repressors

\

+	interactions between regions of chromatin that are physically distant from each other on chromosomes but interact in three-dimensional space within nuclei. 



Description
***********

The methods used for chromatin analysis are all similar in concept, although the chromatin characteristics assayed differ along with the experimental methods used to assay them. `Tsompana and Buck (2014) <https://epigeneticsandchromatin.biomedcentral.com/articles/10.1186/1756-8935-7-33>`_ provide an overview of methods for analysis of chromatin "accessibility", or structural differences that result in differing sensitivity of the DNA in chromatin to modification by various types of proteins. Chromatin immunoprecipitation and sequencing (ChIP-seq) represents another class of experimental techniques, and relies on immunoprecipitation of DNA fragments as a means of enriching DNA sequences. This technique can be used to study any characteristic of chromatin for which a specific antibody is available, ranging from covalent modification of DNA nucleotides (e.g. cytosine methylation) or ubiquitous DNA-binding proteins (e.g. histone acetylation) to the presence of specific DNA-binding proteins (e.g. a transcription factor bound to a transcription promoter region). ChIP-seq, and other methods for analysis of chromatin structure, result in detection of a pool of sequences enriched for sites that meet a set of experimental criteria.  The ratio of "signal", or sequences that meet the experimental criteria, to "noise", or random fragments of genomic DNA that do not meet the experimental criteria, determines the sensitivity and specificity of the experiment. The ENCODE consortium published guidelines for analysis of ChIP-seq data that provide a good overview of potential sources of technical as well as biological variation (`Landt et al, 2012 <http://genome.cshlp.org/content/22/9/1813.full>`_), and a publication by `Thomas et al (2017) <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5429005/>`_ compared peak-calling algorithms in several software packages and identified strengths and weaknesses of different tools. The MACS2 package performed well in these comparisons - `instructions <https://drive.google.com/open?id=1w1OnDmaKV-6e_3bm4pa9WbQQkL3orfM_>`_ for installing that package in a Python virtual environment on a VCL instance are available. A recently-developed procedure called "cleavage under targets and release using nuclease" (CUT&RUN) uses an antibody against a protein of interest, followed by proteinA-coupled micrococcal nuclease treatment to cut DNA on either side of the bound protein, and is reported to have high sensitivity and low background (`Skene et al, 2018 <https://doi.org/10.1038/nprot.2018.015>`_). The level of background from this approach is so low that software designed for analysis of ChIP-seq data is not optimal for CUT&RUN data, so new analytical approaches have been developed (`Meers et al, 2019 <https://www.ncbi.nlm.nih.gov/pubmed/31300027>`_).

\

One advance that has had major impacts on high-throughput sequencing library preparation is the application of a bacterial transposase enzyme to fragment DNA and attach sequencing adapters to the fragments (`Adey et al, 2010 <http://genomebiology.biomedcentral.com/articles/10.1186/gb-2010-11-12-r119>`_). This approach works well for construction of libraries from genomic DNA, but is particularly well-suited to experiments with very small quantities of DNA (sub-picogram amounts, `Picelli et al, 2014 <http://genome.cshlp.org/content/24/12/2033.full>`_), and has been adapted for use in experiments to explore chromatin structure (`Buenrostro et al, 2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3959825/>`_; `Gabdank et al., 2016 <http://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-016-2596-3>`_).

\

Eukaryotic chromosomes exist in vivo as tightly-packed complexes of DNA and proteins, and high-throughput sequencing methods for exploring the three-dimensional structure of those complexes were developed several years ago (`Lieberman-Aiden, et al., 2009 <http://www.sciencemag.org/content/326/5950/289.full>`_). Few genome assemblies are completely finished, without gaps or errors, and the three-dimensional interactions of chromatin within nuclei has proven informative in evaluating the accuracy of genome assemblies and determining the phase of linkage of sequence variants at long distances within individual eukaryotic chromosomes or individual genomes in metagenomic studies (`Burton et al, 2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4117202>`_; `Kaplan and Dekker, 2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3880131/>`_; `Selvaraj et al,2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4180835/>`_). A 2017 publication (`Dudchenko et al, 2017 <http://science.sciencemag.org/content/356/6333/92.long>`_) described a new approach to using 3-dimensional contact data for building chromosome-scale scaffolds of genome assemblies, and demonstrated the method on both a well-studied human genome and on genomes of two mosquito species. This method has been used to improve the contiguity of the barley genome assembly (`Mascher et al, 2017 <https://www.nature.com/articles/nature22043.pdf>`_).


Key Facts
*********

The analysis of genomic events must consider the nature of expected events, as well as sources of technical and biological variation. A key question is whether the event of interest occurs at discrete sites (such as a transcription factor binding to gene promoter sequences) or varies across broad regions (such as histone methylation or acetylation). The number and size of regions at which events occur has a significant impact on the signal-to-noise ratio of the experiment, and therefore a strong influence on the number of sequencing reads required to reach adequate coverage to allow meaningful statistical analysis of potential differences. Analyzing genomic events as reported by a collection of DNA sequence reads typically involves 'normalization'  or adjustment of the data to account for differences in the numbers of reads obtained from different samples. This step is critical because the objective of the experiment is to identify differences in the frequency of detection of different regions of the genome under different experimental conditions, and estimates of the frequency of detection can be biased if the number of reads obtained differs under different experimental conditions. If the objective is to compare different kinds of events, such as binding of transcription factors relative to regions of histone acetylation, the challenge for normalization becomes greater, because the nature of the events is so different.



Exercises
*********

1.	A brief introduction to chromatin immunoprecipitation-sequencing experiments is presented in the `IntroToChIPseq.pdf <https://drive.google.com/open?id=1Lqz2pFuUInB6P8Rcs2n-mxqLAyQlK8xh>`_ document.

\

2.	An exercise using Galaxy, an on-line sequence analysis resource with a graphical user interface, is described in the `Tutorial_ChIPseqOnGalaxy_2020.pdf <https://drive.google.com/a/ncsu.edu/file/d/1pq9CZ6OOYvchs6lK1-rUAjLTL2nCTGFl/>`_ document. This uses aligned reads in BED format, which is not a file format directly produced by most read alignment programs. Instead, the BAM files that are the direct output of alignment programs must be converted into BED files using a program designed for that conversion, such as BEDtools. The sample datasets used in this exercise are a subset of the data described by `Ross-Innes et al (2012) <http://www.nature.com/nature/journal/v481/n7381/full/nature10730>`_; reviewing that publication will give you an overview of how the ChIP-seq analyses conducted in the exercise fit into the overall biology of the experimental system and the biological conclusions drawn by the authors. The public Galaxy server can be slow or unavailable, depending on network traffic, local computational load, and hardware maintenance issues, but offers a free portal to a wide variety of NGS analysis software tools. As an alternative, the data required to complete the ChIP-seq tutorial has been saved in the archive `chipseq <https://drive.google.com/open?id=1eQ6DScDMfhyFlOtZ50T9_AX45u0jqg0O>`_. A script file, `chip.script.sh <https://drive.google.com/open?id=1jwfWj2xIBFImdArjdGMke4_0kzP5oayP>`_, contains commands to execute the same set of analyses as the Galaxy tutorial, but using software installed on the VCL machine image rather than the Galaxy server. Execution of this script should require only entering the path to the script at a terminal prompt; the script will create a directory called chipseq in the home directory that contains output files. Running the script is not as informative as working through the step-by-step exercise in the Tutorial_ChIPseqOnGalaxy.pdf document, but reading the tutorial document and executing the script commands one at a time would be a good compromise offering the speed of local computation and the step-by-step approach of the Galaxy tutorial.

\

3. The BED file format is commonly used to describe the locations at which peaks of sequence reads mark likely locations of immuno-reactive complexes (DNA modifications or protein binding), and the bedtools program is a powerful tool for analysis and manipulation of such files. Bedtools can be installed from the Ubuntu software repository, and a `tutorial <http://quinlanlab.org/tutorials/bedtools/bedtools.html>`_ with guided exercises using bedtools and DNAseI-hypersensitivity data from `Maurano et al (2012) <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3771521/>`_ is available. The `Integrative Genome Viewer <https://www.broadinstitute.org/igv/>`_ is a tool for visualizing genomic data, and provides a graphic interface for exploration of experimental results; the bedtools tutorial includes some visualization steps as examples. A video-guided tutorial (2 hours, ~130mb) is available for download from google drive with `this link <https://drive.google.com/open?id=1dNpEHkLG5-cg0AT17sYyuit5z7EUiYDq>`_.

\

4.	Evaluating data for potential bias and other quality issues is an important part of all experiments. `Meyer and Liu (2014) <http://www.nature.com/nrg/journal/v15/n11/full/nrg3788.html>`_ discuss approaches for identifying and dealing with bias in sequencing datasets, and `Diaz et al (2012) <http://genomebiology.com/2012/13/10/r98>`_ describe a software package (CHip-seq ANalytics and Confidence Estimation, or `CHANCE <https://github.com/songlab/chance/downloads>`_) designed to help experimenters analyze sequencing data.


Additional Resources
********************

+ `De novo assembly of the Aedes aegypti genome using Hi-C yields chromosome-length scaffolds. <http://science.sciencemag.org/content/356/6333/92.full>`_ Dudchenko et al, Science 356:92-95, 2017

\

+ `A comprehensive comparison of tools for differential ChIP-seq analysis. <http://bib.oxfordjournals.org/content/early/2016/01/12/bib.bbv110.full.pdf+html>`_ Steinhauser et al., Briefings in Bioinformatics 1:14, 2016.

\

+ `Identifying and mitigating bias in next-generation sequencing methods for chromatin biology. <http://www.nature.com/nrg/journal/v15/n11/full/nrg3788.html>`_ Meyer and Liu, Nature Reviews Genetics 15:709  721, 2014

\

+ `Important biological information uncovered in previously-unaligned reads from ChIP-seq experiments. <http://www.nature.com/srep/2015/150302/srep08635/full/srep08635.html>`_ Ouma et al, Scientific Reports 5:8635, 2015  -- *This article highlights the differences among alignment programs in ability to map reads with multiple mismatches to the corresponding genomic region, and reports that the SHRiMP alignment program has the highest sensitivity of the programs compared. Using this program with reads that fail to align to the target genome using Bowtie, the authors were able to recover additional useful data and identify additional target protein binding sites.* 

\

+ `CHANCE: comprehensive software for quality control and validation of ChIP-seq data. <http://genomebiology.com/2012/13/10/r98>`_ Diaz et al, Genome Biology 13:R98, 2012

\

+ The lab `home page <http://liulab.dfci.harvard.edu/MACS/00README.html>`_ for the program Model-based Analysis of Chip-Seq data (MACS), and the Github `software download <https://github.com/taoliu/MACS>`_ page. 

\

+ The `home page <http://galaxyproject.org/>`_ for the Galaxy workspace development team

\

+ `Chip-seq analysis in R (CSAR): an R package for the statistical detection of protein-bound genomic regions. <http://www.plantmethods.com/content/7/1/11>`_ Muiño et al, Plant Methods 7:11, 2011 

\

+ `Normalization, bias correction, and peak calling for ChIP-seq. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342857>`_ Diaz et al, Stat Appl Genet Mol Biol 11:10.1515/1544-6115.1750, 2012

\

+ `Practical guidelines for the comprehensive analysis of ChIP-seq data. <http://www.ploscompbiol.org/article/info%3Adoi%2F10.1371%2Fjournal.pcbi.1003326>`_ Bailey et al, PLoS Comput Biol  9(11):e1003326, 2013 

\

+ `Refined DNAse-seq protocol and data analysis reveals intrinsic bias in transcription factor footprint identification. <http://liulab.dfci.harvard.edu/publications/NatMethods13_Dec8.pdf>`_ He et al, Nature Methods 11(1):73  78, 2014

\

+ `Measuring reproducibility of high-throughput experiments. <http://arxiv.org/pdf/1110.4705.pdf>`_ Li et al, Annals of  Applied Statistics 5: 1752  1779, 2011.

\

+ `Mapping chromatin interactions with 5C technology. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3874844/>`_ Ferraiuolo et al, Methods 58: 10.106/j.ymeth.2012.10.011, 2012

\

+ `Biological implications and regulatory mechanisms of long-range chromosomal interactions. <http://www.jbc.org/content/288/31/22369.long>`_ Wei et al, J Biol Chem 288: 22369  22377, 2013

\

+ `An estrogen-receptor-alpha-bound human chromatin interactome. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2774924/>`_ Fullwood et al, Nature 462: 58  64, 2009

\

+ `The hitchhiker's guide to Hi-C analysis. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4347522/>`_ Lajoie et al., Methods 72: 65  75, 2015.

\

+ `The Variant Call Format and VCFtools. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3137218/>`_ Danecek et al, Bioinformatics 27: 2156 - 2158, 2011

\

+ `Variant Tool Chest: an improved tool to analyze and manipulate variant call format (VCF) files. <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4110736/>`_ Ebbert, et al., BMC Bioinformatics 15 suppl. 7: S12, 2014




Last modified 25 March 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
