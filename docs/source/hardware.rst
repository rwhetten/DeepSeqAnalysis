.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu 



Computing Hardware
==================

Global overview
***************

1. Accounts on the HPC are available to those with an NCSU Unity ID - see `Get Access <https://projects.ncsu.edu/hpc/Accounts/GetAccess.php>`_ for information.
2. Connect to the HPC via login.hpc.ncsu.edu using PuTTY for a command-line interface
3. Create a job submission script file that contains the commands you want to execute
4. Submit the job script to the appropriate queue and wait until the job is complete
5. Transfer the output data back to your office workstation for further analysis, or write another job submission script to carry out more analysis on the HPC.

Job submission and management
*****************************

A tool called Load Sharing Facility (LSF) is used to manage the queues of submitted computing jobs on the HPC cluster. See `Running Applications <https://projects.ncsu.edu/hpc/Documents/LSF.php>`_ for more information on batch job submission with LSF, and the factors considering in prioritizing submitted jobs in the queue. More information is available at the `FAQ for HPC users <https://projects.ncsu.edu/hpc/Documents/HowTo.php>`_; additional documentation on LSF commands can also be found via Google searches.

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

	- Similar to other shell scripts, batch job scripts start by specifying the shell that will process the script, e.g. #!/bin/bash or another shell.
	- The next lines specify options for the batch submission process, including details like the number of compute cores required, the amount of time to be allocated to the batch job, the amount of memory needed, the job name, and the output files to which errors and job outputs should be written.
	- After all the options are specified, then the code that actually loads software modules and executes the desired programs is included in the script. Depending on the number of different tasks to be executed, there may be a need to load multiple software modules and ensure compatibility among the versions of different software packages to be used in the analysis.


Setting up NCSU AFS and Drive Access
***********************************************
	- `AFS filespace and NCSU Drive <https://oit.ncsu.edu/my-it/filespace/ncsu-drive>`_ filespace are two different storage options that are available to NCSU campus community members (students, staff, and faculty). Access to these storage volumes is enabled on the VCL instances used in class. Access to AFS filespace is enabled by default and a directory called AFS is created in the home directory of each user; the NCSU Drive space can be mounted by entering the command **mount.mydrive** in a terminal window and entering the appropriate Unity password in response to the prompt, after which the NCSU Drive space is available at the path **/mnt/mydrive**. Both of these storage volumes can also be accessed from Windows or Mac desktop or laptop computers; the OIT webpage linked above has information on how to set up this access. Saving work from the VCL instance to these non-volatile storage options is important if you want keep any files produced during a VCL work session, as all user-created files saved on the virtual machine instance will be lost when the work session is terminated.


Last modified 5 January 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.

