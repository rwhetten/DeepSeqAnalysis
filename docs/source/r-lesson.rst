.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


R and R Studio
==============


Objective
*********

Provide an opportunity to learn basic R usage with lessons from Software Carpentry, and applications of R and Bioconductor to genomic data analysis with lessions from Data Carpentry. R (v 4.0.4), RStudio (v 1.4.1103), and Bioconductor (v. 3.12)  are already installed on the VCL image. If you log in using a Remote Desktop connection, you can find RStudio under the Applications menu in the Devlopment category. If you normally log into a VCL instance using SSH, then you have a choice of either using R in the terminal window on the VCL instance, or using RStudio running on the computer that you use to connect to the VCL. The Software Carpentry and Data Carpentry tutorials are written with the assumption that you will be using RStudio, so if you choose to work in a terminal through SSH to the VCL, you will not be able to carry out all the exercises in the tutorials exactly as they are written.


Background
**********

Base R is designed to load all data into RAM, and this works fine for small datasets. Large genomic datasets aren't suitable for this model of memory management, however, so a new approach to data access was developed for genomic analysis in R. The Bioconductor environment provides tools that allow R to access specific parts of large datasets without loading the entire file into memory, and a large number of R packages for genomic data analysis are now available through the Bioconductor package management system. `Materials for a two-day workshop on R and Bioconductor for genomic data analysis <https://bioconductor.org/help/course-materials/2016/BiocIntro-May/>`_ are available - the introductory material reviews basic R functions and data types, then expands into Bioconductor-specific topics. 

More links to conference presentations and workshop materials related to Bioconductor are available on the `Bioconductor Courses and Conference Talks <https://bioconductor.org/help/course-materials/>`_ web page - note that each set of presentation materials is linked to a specific version of Bioconductor and R in the right-most column, so the most recent course materials will assume that you have the corresponding versions of Bioconductor and R installed on your system if you plan to carry out the exercises demonstrated. 


Workshop Links
**************

`Software Carpentry <http://swcarpentry.github.io/r-novice-gapminder/>`_ is an introductory tutorial for R and RStudio that is not focused on genomic data, but introduces R data structures, flow control, graphics and visualization tools, and data manipulation methods. 


`Data Carpentry for Genomics <http://www.datacarpentry.org/lessons/#genomics-workshop>`_ is an introduction to the bash command line and methods for read QC, trimming, alignment, and analysis that is similar to exercises we have already done in class, although they use different software for some tasks (e.g. Trimmomatic rather than bbduk.sh for trimming and quality-filtering reads). This is a good tutorial to work through if you want to review the concepts and steps covered in the first few weeks of our class, from an independent perspective.


Additional Resources
********************

+ Orchestrating high-throughput genomic analysis with Bioconductor. Huber et al, Nature Methods 12:115, 2015 `PubMed Central <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4509590/>`_ *This paper is the recommended citation for those who publish research results developed with the use of Bioconductor packages. It is not the most useful source of information about how to analyze data using Bioconductor, but instead provides a global overview of the goals and strategies of the development team.*

\

+ Ten simple rules for creating a good data management plan. Michener WK. PLoS Comput Biol 11(10): e1004525, 2015. `Full Text <https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004525>`_ *This paper is focused on meeting the requirements of funding agencies for data management plans associated with specific research projects. The guidelines presented are not dependent on any specific mechanism for organizing and managing data on a particular computing platform, but instead on the larger-scale and longer-term questions of how the data will be made available to the larger scientific community upon completion of the research.*

\

+ A quick guide for organizing computational biology projects. Noble WS. PLoS Comput Biol 5(7): e1000424, 2009 `Full Text <https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424>`_ *This paper provides one perspective on factors to consider in creating a directory hierarchy for storing data, scripts, analysis results, and other information related to computational biology projects. A Google search for 'bioinformatics directory structure' returns many links to pages with other perspectives, and personal preferences are important in determining what will work best for any particular person. Uniformity of naming conventions is one unifying theme, however, because having a consistent system of naming directories and files makes it easier to manage data with bash scripts and regular expressions.*

\

+ `R & Bioconductor Manual <http://manuals.bioinformatics.ucr.edu/home/R_BioCondManual>`_ by Thomas Girke from UC Riverside. *This webpage provides a very complete introduction to R and Bioconductor, with specific examples of many useful tools and analytical methods applied to genomic datasets.*



Last modified 4 March 2021.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_
