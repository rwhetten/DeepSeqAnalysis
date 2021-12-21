.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


Semester Overview, 2022
=======================


.. image:: /Images/syllabus_logo.jpg
Image credit: `Lilian Matallana <https://www.linkedin.com/in/lilian-matallana-21704474/>`_




			**Class meetings are in Jordan Hall 6117 from 8:30 to 10:20 am on Mondays, Wednesdays, and Fridays.**

				The `Biostar Handbook <https://www.biostarhandbook.com/>`_ is a resource for much of the reading.

				A Slack channel is available for questions and discussion.
			
				Will Kohlway (will_kohlway at ncsu.edu) is the teaching assistant for the course.


Course Schedule 
***************

 **Week and Dates**	Topic [Relevant Biostar Handbook chapters, links to other resources]

	**Week 1, 10 – 14 Jan**	Introduction to bioinformatics, Linux, and the command-line interface [1, 3, `The Linux Command Line <http://linuxcommand.org/index.php>`_, `Data Science at the Command Line <https://datascienceatthecommandline.com/2e/index.html>`_]

	**17 Jan**       Martin Luther King, Jr Day - University closed, no classes
	
	**Week 2, 19 - 21 Jan**	Sequencing instruments [12, `Performance Assessment of DNA Sequencing Platforms <https://rdcu.be/cCCQt>`_], experimental design, and introduction to the NC State HPC
	 	        	
	**Week 3, 24 - 28 Jan**	Data preprocessing and quality control [14] and sequence read alignment [28]	 

	**Week 4, 31 Jan - 4 Feb**	Transcriptome assembly  [25 - general introduction; `Best Practices for DeNovo Transcriptome Assembly with Trinity  <https://informatics.fas.harvard.edu/best-practices-for-de-novo-transcriptome-assembly-with-trinity.html>`_ ]
	
	**Week 5, 7 - 11 Feb**	Genome assembly [25]

	**Week 6, 14 - 18 Feb**	Re-sequencing, alignment, structural variation [18] 

	**Week 7, 21 - 25 Feb**	Discovery and genotyping of genetic variation [20, 21]	 

	**Week 8, 28 Feb - 4 Mar**	R and R Studio -  Software Carpentry `Programming with R <http://swcarpentry.github.io/r-novice-inflammation/>`_ and `R for Reproducible Scientific Analysis <https://swcarpentry.github.io/r-novice-gapminder/>`_, Data Carpentry `Genomics Workshop <https://datacarpentry.org/lessons/#genomics-workshop>`_

	**Week 9, 7 - 11 Mar**	Transcriptome analysis: differential gene expression, annotation [22]	

	**Week 10, 14 - 18 Mar**	Spring Break - no classes	

	**Week 11, 21 - 25 Mar**	Genome analysis: ChIP-seq, DHS-seq, 3-D conformation [23, 24, CLC GWB `ChIP sequencing tutorial <https://resources.qiagenbioinformatics.com/tutorials/ChIP-seq_peakshape.pdf>`_]	 

	**Week 12, 28 Mar - 1 Apr**	Linux command-line tools: awk, sed, and bash [`Bioawk Basics <https://bioinformaticsworkbook.org/Appendix/Unix/bioawk-basics.html>`_; `Sed Basics <https://bioinformaticsworkbook.org/Appendix/Unix/unix-basics-4sed.html>`_; `Using bash in bioinformatics <https://people.duke.edu/~ccc14/duke-hts-2018/cliburn/Bash_in_Jupyter.html>`_; `The Art of Bioinformatics Scripting <https://www.biostarhandbook.com/books/scripting/index.html>`_]
	
	**Week 13, 4-8 Apr**	CLC Genomics Workbench - data QC and pre-processing	 

	**Week 14, 11 - 15 Apr**	CLC Genomics Workbench - Expression analysis using RNA-seq data [`tutorial <https://resources.qiagenbioinformatics.com/tutorials/RNASeq-droso.pdf>`_]	 

	**Week 15, 18 - 22 Apr**	CLC Genomics Workbench - Paired-end short-read genome assembly [`tutorial <https://resources.qiagenbioinformatics.com/tutorials/De_novo_assembly_paired_data.pdf>`_]; Long-read assembly with short-read polishing [`tutorial <https://resources.qiagenbioinformatics.com/tutorials/De_Novo_Assembly_Using_Long_Reads_and_Short_Read_Polishing.pdf>`_]	 

	**25 Apr**	Last day of class - questions, review, summary	 


General background information and course resources
***************************************************

+	General advice on `troubleshooting <troubleshooting.html>`_
+	`Course syllabus <https://drive.google.com/file/d/1wlAVNHiPSLiZ6yxojj9iB6CNZSpqw6WG/>`_
+	Lior Pachter's list of sequencing-based assays: `\*Seq <https://liorpachter.wordpress.com/seq/>`_
+	`DNA Sequencing Methods Collection <https://drive.google.com/file/d/1FCe3rnHDiwUUu6pSZ9LkDuDDyYouFyAS/>`_ - Illumina compilation of published methods
+	`For All You Seq - DNA <https://drive.google.com/file/d/1lJ9EPzqG71pPOkSpHSNLFpoh23JIjMDC/>`_ and `For All You Seq - RNA <https://drive.google.com/file/d/1aViVPAgLPkOEUiDAaHvcp-ftunZTk-zF/>`_ are Illumina posters that give brief graphical summaries of many different kinds of sequencing assays
+	`The R statistical programming environment <r-materials.html>`_
+	`Course resources and recommended reading <resources.html>`_
+	`Overview slides (old and outdated in some respects) <https://drive.google.com/open?id=10RYNwJXx7gwYCA_o_1u8AtRw465ROjZn>`_
+	Cloud computing with Amazon Web Services: `setting up an AWS account <https://drive.google.com/open?id=1OXA_TAYu2l_--GEAW85eKJCLUtWyqhbN>`_ and `starting an instance <https://drive.google.com/open?id=1U7D7BRfS1LLbWGzJwkBejc8vfyRSPLIc>`_
+	OMICtools software database `publication <http://database.oxfordjournals.org/content/2014/bau069.long>`_ and `website <http://omictools.com/>`_
+	Qiagen webpage of `tutorials <https://www.qiagenbioinformatics.com/support/tutorials/>`_ for CLC Workbench programs
+	`Colib'read project webpage <https://colibread.inria.fr/project/>`_ on reference-assembly-free programs for SNP and indel detection and moress 


A flow-chart overview of DNA sequencing experiments
***************************************************

	.. image:: /Images/Flowchart.jpg 







Last modified 21 December 2021.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
