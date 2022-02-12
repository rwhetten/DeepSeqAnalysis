.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu

.. role:: bash(code)
   :language: bash

Genome Sequencing and Assembly
==============================

Global Overview
***************

De-novo assembly of a complete and accurate genome sequence from high-throughput sequencing data is a challenging computational problem for any genome that contains repeated DNA sequences longer than the typical sequencing read length (`Simpson & Pop, 2015 <http://www.annualreviews.org/doi/abs/10.1146/annurev-genom-090314-050032>`_). The single-copy regions between repeated sequences can be assembled into contiguous stretches of sequences, or "contigs". Construction and sequencing of "mate-paired" sequencing libraries allow retrieval of DNA sequences known to occur at a specific spacing in the genome, which can range from 2 kb to 35 or 40 kb. These data allow linking of contigs into larger "scaffolds" that contain gaps where the exact sequence is unknown but the approximate size is known. "Draft" genome assemblies often consist of many such scaffolds, and the unknown sequences in the gaps within scaffolds can represent half or more of the total length of the scaffolds. The process of "finishing" a genome sequence involves collecting sequence data to fill the gaps in scaffolds and ensure that all contigs are placed in the correct order and orientation relative to each other to form a complete continuous sequence of each chromosome of the genome of interest. This process is difficult and expensive, so few eukaryotic genomes larger than those of fungi are completely finished. Long-read sequencing methods, such as Pacific Biosciences and Oxford Nanopore Technologies single-molecule sequencing, provide reads long enough to bridge across many repetitive regions in eukaryotic genomes, and such long-read data have been used to improve existing assemblies of mammalian genomes (e.g. the gorilla genome, `Gordon et al, 2016 <http://science.sciencemag.org/content/352/6281/aae0344.long>`_) and carry out de-novo assembly of fungal genomes (e.g. the genome of Verticillium dahliae, `Faino et al, 2015 <http://mbio.asm.org/content/6/4/e00936-15.long>`_).

Alternative approaches to scaffolding have been developed, based on the observation that DNA packaged into nucleosomes and higher-order chromatin shows a consistent pattern of long-range interactions both in vivo using nuclei isolated from living cells (`Lieberman-Aiden et al, Science 326:289-293 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2858594/>`_, 2009) or in vitro using DNA-histone complexes prepared from purified DNA and proteins (`Putnam et al, Genome Research 26:342-350 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4772016/>`_, 2016). In the past few years, methods to use these long-range interactions to aid in scaffolding genome assemblies and determining the linkage phase of genetic variants in diploid genomes have been developed (`Burton et al <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4117202/>`_, Nat Biotechnol 31:1119-1125, `Kaplan & Dekker <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3880131/>`_, Nat Biotechnol 31:1143-1147, and `Selvaraj et al <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4180835/>`_, Nat Biotechnol 31:1111-1118, all in 2013; Putnam et al in Genome Research, cited above). 

Another means of detecting long-range linkages among DNA sequences is based on experimental strategies that result in labeling all sequence reads derived from individual long (50 kb to 250 kb) DNA fragments with the same unique barcode sequence, so that reads can be grouped into clusters of known relationships. The first commercially-available system to produce this type of library was from 10x Genomics (`Mostovoy et al <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4927370/>`_, Nat Methods 13:587-590, 2016), but there are now two additional commercial options and a method that can be applied by individual researchers in their own labs. The 10x Genomics system is based on microfluidic technology that creates an emulsion of aqueous droplets in oil, where each droplet contains a different 14-base barcode. The commercial service provided by BGI (`Wang et al <https://genome.cshlp.org/content/29/5/798.full>`_, Genome Research 29:798-808, 2019), the kit now available from Universal Sequencing (`Chen et al <https://www.biorxiv.org/content/10.1101/852947v1.full>`_, bioRxiv 2019), and the research method suitable for individual laboratories (`Redin et al <https://www.nature.com/articles/s41598-019-54446-x>`_, Scientific Reports 9:18116, 2019) all use the Nextera DNA Flex bead-linked transposase kit available from Illumina (`Bruinsma et al <https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-018-5096-9>`_, BMC Genomics 19:722, 2018). These methods are known under the general heading of linked-read library methods, and the groups of reads all derived from the same original DNA fragment and marked with the same barcode are sometimes called "read clouds". In addition to the value of these data for genome assembly, they are also very useful for experimental haplotyping of diploid samples to determine the phase of linkage of variant sites (`Zhang et al <https://academic.oup.com/gigascience/article/8/11/giz141/5643883>`_, Gigascience 8:giz141, 2019). Deciding which of the available technologies to use can be driven by the availability of services, the costs, and the expected benefit of adding additional data types to the genome assembly process. `Etherington et al <https://doi.org/10.1093/gigascience/giaa045>`_ (Gigascience 9:giaa045, 2020) report a comparative analysis of ten genome assemblies made by combining Illumina short-read data, mate-pair or jumping libraries, BioNano optical mapping, and 10x Genomics linked-read data in various combinations, and provide a ranking of the different assemblies in terms of quality (contiguity, correctness, and completeness), cost, and cost per unit of contiguity (N50 per $1000).

Objective
*********

The objective of this session is to introduce participants to important issues to consider in genome sequencing and assembly experiments. Simulation of sequencing reads from a bacterial genome will provide example datasets that will serve as input to an assembly program, and will allow testing the effect of sequencing error rate on assembly quality.

Description
***********

De-novo assembly of short DNA sequence reads into a complete genome reference sequence is a challenging and computationally-intensive task for genomes larger than a few megabases, and can be difficult even for small bacterial genomes that happen to be rich in repeated DNA sequences. The key challenge in assembly is to correctly place DNA segments that occur only once in the genome relative to repeated sequences that occur multiple times.  The Overlap-Layout-Consensus strategy used to assemble the human genome sequence from Sanger sequencing reads  (500 to 900 nt in length) is not feasible for assembly from short reads (50 to 150 nt in length). An alternative approach, based on de Bruijn  graph theory, breaks reads up into short fragments called k-mers, which are oligomers k nt in length, with k typically ranging from 19 to 75 depending on read length. These k-mers can be much more efficiently indexed and analyzed than longer reads, and very efficient mathematical methods are available for solving the problem of ordering k-mers into contiguous sequences (Pevzner et al, 2001). A recent publication described a hybrid approach, in which short paired-end reads are analyzed as k-mers, then extended into "super reads" by searching for unique overlapping k-mer sequences at the ends of each read. This process converts large numbers of short reads into a much smaller number of longer "super reads" that can be assembled using the OLC strategy (Zimin et al, 2013). A follow-up report by `Zimin et al (2017) <https://genome.cshlp.org/content/27/5/787.long>`_ extends the "super-read" concept to allow incorporation of long single-molecule sequence reads from Pacific Biosciences or Oxford Nanopore sequencing platforms to form "mega-reads", and describes assembly of the *Aegilops tauschii* genome to a higher degree of contiguity than previously reported.

Key Facts
*********

The length and number of repetitive sequences in a particular genome determine the sequencing strategy to produce data likely to allow a relatively complete assembly. The objective is to have good coverage of the genome with pairs of reads that are far enough apart to guarantee that both reads of a pair are not within the same repetitive sequence element.  If one read is within a repetitive element and the other read is in flanking sequence that is unique in the genome, then that read pair provides evidence locating one copy of the repetitive element within a specific unique-sequence region in the genome. Different genomes have differing lengths and arrangements of repetitive DNA sequences in the genome, so different strategies may be required for library construction and sequencing.

Different approaches have been proposed to evaluate the quality and completeness of de novo genome assemblies. `Assemblathon-1 (2011) <http://genome.cshlp.org/content/early/2011/09/16/gr.126599.111.abstract>`_ and `Assemblathon-2 (2013) <https://gigascience.biomedcentral.com/articles/10.1186/2047-217X-2-10>`_ were multi-investigator projects to compare the utility of different software tools and analytical approaches to genome assembly. `QUAST <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3624806/>`_ and `REAPR <https://genomebiology.biomedcentral.com/articles/10.1186/gb-2013-14-5-r47>`_ are software tools for assessment of the quality of genome assemblies, both published in 2013. QUAST offers many metrics of assembly quality based on similarity to an existing reference genome assembly, and some metrics than can be applied to new genome assemblies that lack any existing reference sequence. REAPR assesses the degree of correctness of an assembly based on results of re-mapping of paired-end reads back to the assembly and finding regions that don't match the expected distribution of paired-end sequences - see the `manual <https://drive.google.com/open?id=1OT7un7RT8OrX_937v6nVUT0co75rcPm->`_ for details. REAPR is installed on the VCL image, so it is available for use on instances running on the VCL. `BUSCO <https://academic.oup.com/bioinformatics/article/31/19/3210/211866/BUSCO-assessing-genome-assembly-and-annotation>`_, described in a 2015 publication, assesses assembly completeness by testing for the presence of conserved genes found in many existing genome assemblies of species from the relevant phylogenetic realm to the assembly being tested. The authors of the BUSCO publication maintain a `website <http://busco.ezlab.org/>`_ where data for evaluation of genome assemblies from various taxa of organisms can be downloaded.

+ Sequencing library recommendations by Gnerre et al. (2011) for mammalian genomes:

  + Create both paired-end (180 bp insert, 2x100-nt reads) and mate-pair libraries of different (3 kb, 6 kb and 40 kb)  insert lengths (see `illumina's webpage <https://www.illumina.com/science/technology/next-generation-sequencing/mate-pair-sequencing.html>`_ for information on mate-pair libraries)

+ Variant discovery/genotyping

  + SNPs vs structural variants: SNPs are more abundant as sites, but insertion/deletion (indel) and rearrangement events can affect more nucleotides genome-wide
  + Common alleles vs rare: common alleles are easier to detect and effects can be estimated accurately; rare alleles can be so hard to find that specific strategies are needed to identify sufficient numbers of individuals to provide statistical power to estimate SNP effects
  + Barcoding works well for genotyping specific individuals at SNPs with common alleles: pooled samples work well for identifying rare variants and estimating allele frequencies.

Exercise - assembly of a bacterial genome from simulated Illumina 100-nt PE reads
*********************************************************************************

The `GenomeAssembly shell script <https://drive.google.com/open?id=1wLU75DflXTdHeA2oD51ppeDHaLdOzDtr>`_ will guide the exercises for this class. You can download an `archive <https://drive.google.com/open?id=1PWLCABfrEpxAeG0XOBwPsDBE_KxBqG3N>`_  of the bacterial genome and simulated reads from the web page, or use the following command in a terminal session:

::
   
   wget http://152.7.176.221/ExerciseData/archives/DPC4571.tgz
   


+ Simulation of paired-end short reads from a bacterial genome sequence can be done with the GemReads.py program used previously, but that process takes some time.  Two files containing simulated 100-nt paired-end reads from the *Lactobacillus helveticus* strain DPC4571 genome are included in the DPC4571.tgz archive mentioned in the previous paragraph: `sim.r1.fq.gz <https://drive.google.com/open?id=129qylzArUm3-K6-Rv8ORKqBwURuzwu5m>`_ and `sim.r2.fq.gz <https://drive.google.com/open?id=1ETW5KbnT7MTmxznzJSaUrTEKkhZmb-7A>`_. The GemReads.py program is installed on the VCL instance if you want to use it to simulate reads from another DNA reference sequence, or simulate reads with different characteristics from the example bacterial genome we are using.

\

+ Use the *df* (remember "disk free") command to see how much free space is left on your VCL instance - this is a useful practice before doing anything that generates large output files, because it is frustrating to start a large computing job and have it fail due to a lack of disk space to store output files.

\

+ Map the simulated reads back to the reference genome sequence using the BWA aligner - execute the commands *bwa index* and *bwa mem* at a terminal prompt for an overview of the command-line options of the commands to create an index of the reference genome sequence and align the simulated reads to it, or read the `manual <http://bio-bwa.sourceforge.net/bwa.shtml>`_ to learn more of the details about how to carry out alignment of short reads to a reference genome. NOTE: BWA programs read from gzipped files, so you do not need to un-gzip the reference genome (`DPC4571.fasta.gz <https://drive.google.com/open?id=1Aj85OISJucpTYg5jwMhhAldwpMAlmzvZ>`_) sequence file, or the `sim.r1 <https://drive.google.com/open?id=129qylzArUm3-K6-Rv8ORKqBwURuzwu5m>`_ and `sim.r2 <https://drive.google.com/open?id=1ETW5KbnT7MTmxznzJSaUrTEKkhZmb-7A>`_ sequence read files. By default, BWA writes SAM-format output to STDOUT (the screen), so you need to redirect that to a file or another command in order to save it. In order to save space, it is most efficient to pipe the SAM output to samtools sort to sort the BAM file so it is ready for use in other downstream applications. The BWA and samtools packages are installed in the search path, so you can use these programs without specifying a complete path to the executable files. Entering either the *bwa mem* or the *samtools sort* command at a terminal prompt without other arguments will return a brief help message describing the key parameters and options available for those programs.

\

+ The MaSuRCA assembler tgz archive has already been unpacked, compiled, and installed in the /usr/local/MaSuRCA-4.0.1/ directory of the VCL machine image.

\

+ Use the MaSuRCA assembler to assemble the simulated reads into a genome assembly, following the instructions given in the MaSuRCA `Quick Start Guide <https://drive.google.com/open?id=1hvUumBdd9LLWlxAzg6NMuSv2gLYYjabk>`_. The average insert size and standard deviation of insert sizes of the simulated paired-end reads is available from the information scrolled to the screen by the BWA mem program during the alignment process, or in the `KmerCounting_ErrorCorrection.sh <https://drive.google.com/open?id=101JatUPQIAtjtRUkYw4V6CZCS03KuKqB>`_ script in the section that describes the GemReads.py command used to simulate the reads.

\

+ Comparison of the genome assembly to the genome reference sequence is possible using whole-genome alignment with `MUMmer v.3 <http://mummer.sourceforge.net/manual/>`_. This package of programs is installed in the /usr/local/MaSuRCA-4.0.1/bin/ directory; look at the list of programs and type
  :code:`nucmer -h` at a terminal prompt to see the options available for the nucmer sequence alignment program.


+ Assembly quality metrics and Assemblathon-1: `Outline and notes <https://drive.google.com/open?id=1FPqLshMXQEBJNpX6AqpvoMuMP4A8ZMzL>`_

\



Additional Resources
********************

+ Etherington et al. (2020) Sequencing smart: *De novo* sequencing and assembly approaches for a non-model mammal. Gigascience 9:giaa045 `Full Text <https://doi.org/10.1093/gigascience/giaa045>`_ *A comparative analysis of the quality of genome assemblies generated using short-read Illumina data either from PCR-free libraries or from 10x Genomics linked-read libraries, assembled with different assembler programs and combined with different types of long-distance linking information. A good example of how to assess the quality of genome assemblies.*

\

+ Hunt, et al. (2013) REAPR: a universal tool for genome assembly evaluation. Genome Biol 14:R47 `Full Text <https://doi.org/10.1186/gb-2013-14-5-r47>`_ *Recognition of Errors in Assemblies using Paired Reads (REAPR) is a software tool for evaluation of the correctness and completeness of a genome assembly using only paired-end Illumina sequencing data, designed to provide an estimate of the likelihood of correctness for each base in a genome assembly, as well as identifying positions that are likely to be mis-assembled*

\

+ Rhie, et al. (2020) Merqury: reference-free quality, completeness, and phasing assessment for genome assemblies. Genome Biol 21:245 `Full Text <https://doi.org/10.1186/s13059-020-02134-9>`_ *Another software tool for reference-free quality assessment of genome assemblies, with the added capability of evaluating phased diploid assemblies, and including a variety of graphical outputs for comparative analyses*

+ Zimin A, et al. (2013) The MaSuRCA genome assembler. Bioinformatics 29:2669–2677. `Publisher Website <http://bioinformatics.oxfordjournals.org/content/29/21/2669.full>`_ *This paper describes a novel strategy for local assembly of Illumina or other short paired-end sequencing reads into "super reads" that can then be assembled using a modified version of an Overlap - Layout - Consensus assembler.*

\

+ Veeckman, E., et al. (2016) Are we there yet? Reliably estimating the completeness of plant genome sequences. Plant Cell 28:1759-1768 `Publisher Website <http://www.plantcell.org/content/28/8/1759.long>`_  *This paper provides an overview of metrics for assessment of the completeness of de-novo genome assemblies, along with a discussion of potential sources of bias of different approaches.*

\

+ Khelik et al, (2017) NucDiff: in-depth characterization and annotation of differences between two sets of DNA sequences. BMC Bioinformatics 18:338. `Publisher Website <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-017-1748-z>`_  *This paper describes a software package that uses results from Mummer v3 Nucmer, delta-filter & show-snps programs to classify sequence differences, which are presented in GFF3 format so they can be visualized in a genome browser.*

\

+ Baker, M. (2012) De-novo genome assembly - what every biologist needs to know. Nature Methods 9:333-337 `Publisher Website <http://www.nature.com/nmeth/journal/v9/n4/full/nmeth.1935.html>`_

\

+ Gnerre S, et al. (2011) High-quality draft assemblies of mammalian genomes from massively parallel sequence data. Proc Natl Acad Sci USA 108:1513–1518. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3029755/>`_  *This paper provides recommendations for different types of Illumina libraries and appropriate depths of sequencing for best results with the ALLPATHS assembler. While this approach was the state-of-the-art in genome assembly for a period of time, it is no longer considered the optimal approach.*

\

+ Salzberg S, et al. (2012) GAGE: A critical evaluation of genome assemblies and assembly algorithms. Genome Research 22:557–567. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3290791>`_  *This paper describes a set of experiments comparing different assembly programs on four genomes, and provides useful insights into the challenges of genome assembly.*

\

+ Magoc T and Salzberg S. (2011) FLASH: Fast Length Adjustment of Short Reads to improve genome assemblies. Bioinformatics 27:2957–2963. `PubMedCentral <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3198573/>`_

\

+ Pevzner PA, et al. (2001) An Eulerian path approach to DNA fragment assembly. PNAS 98:9748-9753. `Full Text <http://www.pnas.org/content/98/17/9748.full>`_


Class Recordings
----------------

+   `Session 10: recorded February 10th 2021 <https://drive.google.com/file/d/1mjBXmBdjrjDufj5e32fd3LUO25qtxU1u/view?usp=sharing>`_ (this link is video and audio). A Transcript of recording of the video `is also available <https://drive.google.com/file/d/18KZf-g8xu5NnkkbXK5y5-1TQ8xMtx-1i/view?usp=sharing>`_.

+   `Session 11: recorded February 12th 2021 <https://drive.google.com/file/d/1Ab0jN7jCTrrgU8Yd_PL4aySslla8BFsT/view?usp=sharing>`_ (this link is video and audio). A Transcript of recording of the video `is also available <https://drive.google.com/file/d/1uGBvBMlgEh-GJcrFVDJ3NHjolMAXgrtX/view?usp=sharing>`_.

+   `Session 12: recorded February 16th 2021 <https://drive.google.com/file/d/1d_PmnGnxFHJpxum2CuJ4tX53-261I_bx/view?usp=sharing>`_ (this link is video and audio). A Transcript of recording of the video `is also available <https://drive.google.com/file/d/1NXu4q-hKDKclVdq5Dg6wyaUD78TMgECV/view?usp=sharing>`_.

Last modified 16 February 2021.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
