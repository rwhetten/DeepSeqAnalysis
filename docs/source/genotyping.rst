.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


Discovering and Genotyping Genetic Variation
============================================



Global Overview
***************

Different individuals of the same species often have slightly different DNA sequences in nuclear and organellar genomes. Single-nucleotide polymorphisms (SNPs) are differences of single nucleotide bases in DNA, and these may occur at frequencies ranging from less than 10-4 to greater than 10-2, depending on the genetic diversity of the species and the divergence among the samples being compared. Sequence variants may also involve multiple adjacent nucleotides (MNPs), and both SNPs and MNPs may be either substitution, insertion, or deletion events. In addition to variation at the level of the nucleotide sequence, structural variation such as inversions and translocations may also be present. The quality of an available reference sequence is an important contributor to analysis of structural variation in genomic sequencing data, and tools have been developed that are reported to work well with fragmented and incomplete draft assemblies (`Wang et al., 2017 <https://academic.oup.com/gigascience/article/6/12/1/4689116>`_).

Objective
*********

The objective of this class session is to describe and practice methods for discovering and genotyping DNA sequence variation in samples drawn either from structured mating designs or from natural populations. The most cost-effective approach to this challenge, for species with large genomes (ie greater than a few hundred megabases) is reduced-representation sequencing, originally carried out using Sanger sequencing (`Altschuler et al, 2000 <http://www.nature.com/nature/journal/v407/n6803/full/407513a0.html>`_). For species with genomes of less than a few hundred megabases, including most microbes as well as many model species and some crop plants, low-coverage whole-genome sequencing can be used as a method of genotyping (e.g. `Andolfatto et al, 2011 <http://genome.cshlp.org/content/21/4/610.full>`_; `Au et al, 2013 <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3750829/>`_; `Huang et al, 2010 <http://www.nature.com/ng/journal/v42/n11/full/ng.695.html>`_) A variety of methods exploiting high-throughput DNA sequencing platforms for reduced-representation strategies have been described in the past several years.



Description
***********

A common strategy for reduced-representation sequencing is based on digestion of genomic DNA with one or two restriction enzymes, followed by ligation of adapters bearing oligonucleotide "barcode" sequences. Individual samples identified by different barcode sequences on the adapters can be pooled together for subsequent size-selection, amplification, and sequencing. The sequence data from different samples are then analyzed and assigned to the respective samples using the DNA sequences of the barcode section of the adapter. This method was developed in parallel by two different groups, and is known as Restriction-site Associated DNA Sequencing (RAD-seq, `Baird et al 2008 <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0003376>`_) by one group and as Genotyping By Sequencing (GBS, `Elshire et al, 2011 <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0019379>`_) by the other group. The original protocols for RAD-seq and GBS were different, as were the implementation strategies, but the two procedures have become more similar over time until now the distinction is more historical than actual. Several alternative methods for recovery of a specific subset of genomic fragment were reviewed by `Mertes et al (2011) <http://bfg.oxfordjournals.org/content/10/6/374.full>`_; among these are hybridization capture, where synthetic oligonucleotide "bait" sequences are used to selectively enrich a sequencing library for target sequences of interest, and various PCR-based methods for selective amplification of a subset of target sequences. 




Key Facts
*********

Repetitive DNA is a significant challenge for restriction-enzyme-based reduced-representation sequencing methods, particularly for species without a reference genome sequence. The choice of restriction enzymes used to reduce genome complexity should be based on the desired numbers of loci, the frequency of restriction sites in repetitive DNA sequences (including organelle genomes), and the expected level of DNA sequence variation. In the absence of a reference genome sequence, empirical studies of the fraction of genomic DNA found in specific size classes in products from digestion with different single-digest and double-digest reactions can be used to estimate the yield of fragments in a double-digest RAD-seq or GBS experiment (`Peterson et al, 2012 <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0037135>`_). If a draft genome assembly of the target species or a related species is available, simulation can be used to compare the expected yield of restriction fragments from enzyme digestion with different single- or double-digest combinations of enzymes (`Herten et al, 2015 <http://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-015-0514-3>`_, `Mora-Márquez et al, 2017 <https://www.ncbi.nlm.nih.gov/pubmed/27288885>`_). Artifacts in identification of SNP and indel variants from short-read sequencing data are common, and different approaches have been taken to develop software that avoids some of these artifacts. Comparisons of different software packages on well-studied real datasets have reported differences among software tools in susceptibility to various types of artifacts (`Li, 2014 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4271055/>`_). `Verdu et al (2016) <http://onlinelibrary.wiley.com/doi/10.1002/ece3.2466/full>`_ reported results of a study to evaluate possible contributions of paralogous or repetitive sequences to a RAD/GBS experiment using the reads2SNPs software of `Gayral et al (2013) <https://doi.org/10.1371/journal.pgen.1003457>`_, and suggest strategies that may be useful to others dealing with similar challenges.

The Variant Call Format (VCF) file type is widely used to store information about locations of genetic variants, although it uses coordinates based on some sort of reference sequence as a means of identifying locations of variant positions. A common starting point for identification of genetic variant positions is a set of BAM files with alignments of sequence reads from several different individuals. Several software packages can analyze such a dataset to identify candidate genetic variants and save the results in VCF format, including `SAMtools mpileup <http://www.htslib.org/workflow/>`_, `Freebayes <https://github.com/ekg/freebayes>`_, and the Genome Analysis Took Kit (`GATK <https://www.broadinstitute.org/gatk/index.php>`_). Formal specifications of SAM, BAM, and VCF file formats are maintained on Github at `https://github.com/samtools/hts-specs <https://github.com/samtools/hts-specs>`_. 



Exercises
*********

A tar archive containing the files for class can be downloaded with the link below.

:code:`ggID='1b8vlLQAhK6lQtACplqu0lEe2y-xXFw40'
echo "The file ID is $ggID"		
ggURL='https://drive.google.com/uc?export=download'  
filename="$(curl --insecure -sc /tmp/gcookie "${ggURL}&id=${ggID}" | grep -o '="uc-name.*</span>' | sed 's/.*">//;s/<.a> .*//')"  
getcode="$(awk '/_warning_/ {print $NF}' /tmp/gcookie)"  
curl --insecure -LOJb /tmp/gcookie "${ggURL}&confirm=${getcode}&id=${ggID}" `

1.	We will complete an exercise in analysis of a reduced-representation sequencing dataset from a linkage mapping population (two heterozygous outbred individuals and 93 F1 progeny) both without the use of a reference genome, and with the use of the reference genome. The `RADseq <https://drive.google.com/open?id=1b8vlLQAhK6lQtACplqu0lEe2y-xXFw40>`_ archive contains an archive of `bamfiles <https://drive.google.com/open?id=1Kku1sschgluviX-xiX8nC_qyLKoCSkB8>`_ for the 95 samples and the reference sequence for `LG2 <https://drive.google.com/open?id=1tuz5QihPMiOTM_Trdux4gpvRVjAj58tE>`_ the spotted gar genome for use in the exercise with a reference genome. The complete genome sequence is available either from NCBI, or from the `Broad Institute <ftp://ftp.broadinstitute.org/pub/assemblies/fish/spottedGar/LepOcu1/L_oculatus_v1.assembly.fasta>`_; I used the Broad Institute version. Only `LG2 <https://drive.google.com/open?id=1tuz5QihPMiOTM_Trdux4gpvRVjAj58tE>`_ is needed, because the sample dataset includes only loci that map to a single linkage group. The `annotation for LG2 <https://drive.google.com/open?id=1XL0_tgdBe5ZqkwflT0N2XKipEoHvIsW9>`_ is in the same directory; this comes from the GFF3 file for the spotted gar genome (available from `Ensembl <http://useast.ensembl.org/Lepisosteus_oculatus/Info/WhatsNew?db=core>`_), for use in identifying SNPs or other variants within or near annotated genes.

\

2.	Sample datasets are available for download for both the `TASSEL GBS pipeline <http://www.maizegenetics.net/tassel>`_ and for the `STACKS <http://catchenlab.life.illinois.edu/stacks/>`_ software package. The TASSEL package is written in Java, and will run on the OpenJDK version available on most Linux distributions, as well as on Windows or Mac computers. TASSEL v5 requires Java 8, which is installed on the VCL machine image as the OpenJDK version, so those interested in using the most recent version of the TASSEL GBS pipeline can download and install that software package. The STACKS software package is written in C++, and can be compiled on Linux or on Mac OSX systems. 

\

3.	After completing the de-novo and reference-based STACKS analyses, additional exercises with the R package `vcfR <https://drive.google.com/open?id=1vKk4mMUUzvzCxxAkDUI9JDAgVO0XXelc>`_ and the command-line tool `VCFtools <https://drive.google.com/open?id=1Az0rrbRvapgg8-TCLVibJy6ACFA4gdHm>`_ are available. A complete `script <https://drive.google.com/open?id=1qqsoR8hDsunahvN214B6N-ycsijvCm4W>`_ for all commands in the VCFtools tutorial is available, but you will learn more by going through the tutorial step-by-step. These tools are useful in filtering, summarizing, and subsetting selected data from VCF files.  Another option is to explore the use of Freebayes, an alternative program for calling SNPs from BAM alignment files for a set of samples. The BAM files used for the samtools mpileup exercise can also be used for a `Freebayes <http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html>`_ run, and the output VCF files compared. To speed up the Freebayes analysis, use the --use-best-n-alleles 4 option to limit the number of possible alleles the program considers at each site. Freebayes uses a Bayesian approach that considers the data from all individuals in a population to identify variant sites in each individual, and will use a list of the 93 BAM files as input for genotyping much as the SAMtools mpileup program does. Type :code:`freebayes -h` at a terminal prompt for detailed instructions on command-line options for Freebayes; the general form of the command to run Freebayes is

::

	freebayes -L <bamfile.list filename> -f <reference FASTA file> -v progeny.vcf  --use-best-n-alleles 4.



\


4.	As with SAM and other file formats for genomic data, the VCF format specifies some columns that are mandatory and must contain particular kinds of data, and allows individual software developers considerable freedom to expand on these required fields by adding additional information. In VCF files, the variable fields are the INFO column (which contains summary data about a specific variant across all samples) and the FORMAT string (which specifies data that is available about a variant for each sample with non-missing data at that site)  at each genotyped sample, as well as the columns (beginning with column 10) that contain data for each locus from individual samples. One of the vignettes for the vcfR package has a nice `overview of the structure of VCF files <https://cran.r-project.org/web/packages/vcfR/vignettes/vcf_data.html>`_, although the examples use R and the vcfR package and may not be useful for those unfamiliar with R.


Additional Resources
********************

Other software packages for analysis of GBS/RAD-seq data have been reported, including Unified Network - Enabled Analysis Kit (UNEAK, `Lu et al 2013 <http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1003215>`_), PyRAD (`Eaton, 2014 <http://bioinformatics.oxfordjournals.org/content/30/13/1844.long>`_), and AftrRAD (Sovic et al, 2015). A key distinction among these is that in the original versions, some (PyRAD and AftrRAD) allow detection of insertion-deletion (indel) variants as well as substitution events, while others (UNEAK, TASSEL, and STACKS) only considered SNP events. Versions of STACKS  after v1.38 (dated April 18, 2016) include the ability to do gapped alignments, and should therefore be able to detect indels in addition to SNPs. Similarly, TASSEL has moved completely to a reference-based analysis format that also allows detection of small indels. Note that a posting to the TASSEL Google group on Feb 12, 2015 announced that the UNEAK package for species without a reference genome available is no longer being developed.


.. image:: /Images/UNEAKnotSupported.png


|

`Slides <https://drive.google.com/open?id=1br-V0sotJK_-hL7kbXAjurt0hVwmx-oD>`_ with an overview of GBS - by Keith Merrill

Software links
______________

+	Bedtools `documentation <http://bedtools.readthedocs.org/en/latest/>`_

\

+	VCFtools `documentation <http://vcftools.github.io/man_latest.html>`_

\

+	STACKS `manual <http://catchenlab.life.illinois.edu/stacks/manual/>`_

\

+	TASSEL v5 GBS pipeline v2 `manual <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline>`_

\

+	simRAD `R package <https://cran.r-project.org/web/packages/SimRAD/index.html>`_

\

+	ddRADseq package `Github repository <https://github.com/GGFHF/ddRADseqTools>`_


Papers:
_______

+	`STACKS: An analysis tool set for population genomics. <http://onlinelibrary.wiley.com/doi/10.1111/mec.12354/abstract>`_ Catchen et al., Molecular Ecology 22:3124-3140, 2013.

\

+	`An SNP map of the human genome generated by reduced representation shotgun sequencing. <http://www.nature.com/nature/journal/v407/n6803/full/407513a0.html>`_ Altshuler et al., Nature 407(6803):513-516, 2000.

\

+	`Optimized filtering reduces the error rate in detecting genomic variants by short-read sequencing. <http://www.nature.com/nbt/journal/v30/n1/abs/nbt.2053.html>`_ Reumers et al, Nature Biotechnol  30:61-68, 2012

\

+	`Detecting ultralow-frequency mutations by Duplex Sequencing. <http://www.nature.com/nprot/journal/v9/n11/full/nprot.2014.170.html>`_ Kennedy et al, Nature Protocols 9:2586-2606, 2014

\

+	`SNP discovery and allele frequency estimation by deep sequencing of reduced representation libraries. <http://www.nature.com/nmeth/journal/v5/n3/full/nmeth.1185.html>`_ Van Tassell, et al., Nature Methods. 5:247-252, 2008.

\

+	`Rapid SNP discovery and genetic mapping using sequenced RAD markers. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0003376>`_ Baird, et al. PLoS ONE 3(10): e3376, 2008.

\

+	`A robust, simple genotyping-by-sequencing (GBS) approach for high diversity species. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0019379>`_ Elshire, et al. PLoS ONE 6(5): e19379, 2011.

\

+	`Development of high-density genetic maps for barley and wheat using a novel two-enzyme genotyping-by-sequencing approach. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0032253>`_ Poland et al., PLoS ONE 7(2): e32253, 2012

\

+	`Double digest RADseq: an inexpensive method for de novo SNP discovery and genotyping in model and non-model species. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0037135>`_ Peterson, et al., PLoS ONE 7(5): e37135, 2012.

\

+	`Switchgrass genomic diversity, ploidy, and evolution: novel insights from a network-based SNP discovery protocol. <http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1003215>`_ Lu et al, PLoS Genet 9(1): e1003215, 2013

\

+	`RESTseq – efficient benchtop population genomics with RESTriction fragment SEQuencing. <http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0063960>`_ Stolle & Moritz,  PLoS ONE 8(5): e63960, 2013.

\

+	`Inferring phylogeny and introgression using RADseq data: an example from flowering plants (Pedicularis: Orobanchaceae). <http://sysbio.oxfordjournals.org/content/early/2013/06/14/sysbio.syt032.full>`_ Eaton & Ree, Syst Biol doi: 10.1093/sysbio/syt032, 2013

\

+	`PyRAD: assembly of de novo RADseq loci for phylogenetic analyses. <http://bioinformatics.oxfordjournals.org/content/30/13/1844.long>`_ Eaton, DA. Bioinformatics 30:1844-49, 2014.

\

+	`GBSX: a toolkit for experimental design and demultiplexing genotyping by sequencing experiments. <http://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-015-0514-3>`_ Herten et al., BMC Bioinformatics 16:73, 2015.

\

+	`AftrRAD: a pipeline for accurate and efficient de novo assembly of RADseq data. <http://onlinelibrary.wiley.com/doi/10.1111/1755-0998.12378/full>`_ Sovic et al,  Mol Ecol Res 15:1163-71, 2015.

\

+	`ddradseqtools: a software package for in silico simulation and testing of double-digest RADseq experiments. <https://www.ncbi.nlm.nih.gov/pubmed/27288885>`_ Mora-Márquez et al ,  Mol Ecol Resour. 17:230-246, 2017.



Last modified 2 February 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
