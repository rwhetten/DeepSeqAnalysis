.. image:: //media/hd02/BIT815/Overview/Figures/NC_State.gif
   :target: http://www.ncsu.edu 

.. image:: //media/hd02/BIT815/Overview/Figures/FERlogo.png
   :target: http://www.cnr.ncsu.edu/fer/ 

Using the HPC for Bioinformatics Computing
==========================================

Global overview
***************

1. Accounts on the HPC are available to those with an NCSU Unity ID - see `HPC Accounts <https://projects.ncsu.edu/hpc//Accounts/Accounts.php>`_ for information.
2. Connect to the HPC via login.hpc.ncsu.edu using PuTTY for a command-line interface
3. Create a job submission script file that contains the commands you want to execute
4. Submit the job script to the appropriate queue and wait until the job is complete
5. Transfer the output data back to your office workstation for further analysis, or write another job submission script to carry out more analysis on the HPC.

Job submission and management
*****************************

A tool called Load Sharing Facility (LSF) is used to manage the queues of submitted computing jobs on the HPC cluster. See `LSF on HPC Cluster <https://projects.ncsu.edu/hpc//Documents/BladeCenter/ClusterLSF.php>`_ for a summary of the factors considering in prioritizing submitted jobs in the queue. More information is available at the `FAQ for HPC users <https://projects.ncsu.edu/hpc//Documents/HowTo.php>`_; additional documentation on LSF commands can also be found via Google searches.

Available software
******************

The most current list of software available on the HPC can be obtained by logging into the HPC and listing the contents of the directory /usr/local/apps - not all the listed programs are related to bioinformatics, but this will allow searching for a specific program of interest. As of March 1, 2016, installed software useful for biological research applications included a mix of open-source and commercial tools - examples are shown here, but the complete list is much longer.

	+------------------------------+---------------------+-----------------------------+
	| abyss-1.0.14                 | asreml2             | BEAST.v1.4.7                |
	+------------------------------+---------------------+-----------------------------+
	| blasr-smrtanalysis           | bowtie2             | bwa                         |
	+------------------------------+---------------------+-----------------------------+
	| circos                       | cufflinks           | cutadapt                    |
	+------------------------------+---------------------+-----------------------------+
	| EIGENSOFT-3.0                | exonerate           | FastQC                      |
	+------------------------------+---------------------+-----------------------------+
	| fastx_toolkit                | java                | maker                       |
	+------------------------------+---------------------+-----------------------------+
	| maq                          | mothur              | mpiblast-1.4.0              |
	+------------------------------+---------------------+-----------------------------+
	| mrbayes-3.1.1                | mrbayes-3.1.2       | MUMmer                      |
	+------------------------------+---------------------+-----------------------------+
	| ncbi-blast                   | ncbi-em64t          | ncbi-sra                    |
	+------------------------------+---------------------+-----------------------------+
	| oases                        | octave-2.1.73       | paup4b10-x86-linux-icc      |
	+------------------------------+---------------------+-----------------------------+
	| paup4b10-x86-linux-icc.orig  | paup4b10-x86-linux  | paup4b10                    |
	+------------------------------+---------------------+-----------------------------+
	| perl, bioperl                | plink               | python-2.6.5                |
	+------------------------------+---------------------+-----------------------------+
	| python-2.4.4                 | R-2.3.1             | raxml                       |
	+------------------------------+---------------------+-----------------------------+
	| RepeatMasker                 | samtools            | SOAPdenovo2                 |
	+------------------------------+---------------------+-----------------------------+
	| sparsehash-1.5.2             | spss                | SQLite                      |
	+------------------------------+---------------------+-----------------------------+
	| sqlite                       | stacks              | tassel                      |
	+------------------------------+---------------------+-----------------------------+
	| tophat                       | trinity             | velvet                      |
	+------------------------------+---------------------+-----------------------------+
 	
Setting up a job submission script
**********************************

	- Similar to other shell scripts - start by specifying the shell that will process the script, e.g. #!/bin/bash or another shell.
	- The next lines specify options for the batch submission process 


Last modified 17 December 2018.
`Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.

