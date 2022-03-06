.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu 



Computing Hardware: The High-Performance Computing Cluster (HPC) at NC State
============================================================================

Global overview
***************

1. Accounts on the HPC are available to those with an NCSU Unity ID - see `Get Access <https://projects.ncsu.edu/hpc/Accounts/GetAccess.php>`_ for information.
2. Connect to the HPC via ssh to your <UnityID>@login.hpc.ncsu.edu using Terminal (macOS) or MobaXterm (Windows) for a command-line interface
3. Create a job submission script file that contains the commands you want to execute
4. Submit the job script to the appropriate queue and wait until the job is complete
5. Transfer the output data back to your office workstation for further analysis, or write another job submission script to carry out more analysis on the HPC.

Job submission and management
*****************************

A tool called Load Sharing Facility (LSF) is used to manage the queues of submitted computing jobs on the HPC cluster. See `Running Applications <https://projects.ncsu.edu/hpc/Documents/LSF.php>`_ for more information on batch job submission with LSF, and the factors considering in prioritizing submitted jobs in the queue. More information is available at the `FAQ for HPC users <https://projects.ncsu.edu/hpc/Documents/HowTo.php>`_; additional documentation on LSF commands can also be found via Google searches.

Downloads and storage access
****************************

Compute nodes on the HPC do not have access to the Internet, so all software and data required for a program to run must be downloaded to local storage before 
submitting a job request to the queue. `Research storage space <https://oit.ncsu.edu/my-it/teaching-research/research-storage/>`_ is available to all NC State faculty, and students working on research under faculty supervision - this space should be used for data and resources that require stable long-term storage and backup. Data that will be used for a brief period and does not need long-term backup can be written to the research group's directory in the /share volume - see the HPC `Data Storage <https://projects.ncsu.edu/hpc/Documents/Storage.php>`_ page for more details. Databases to be used by programs, such as custom BLAST databases for nucleotide or protein similarity searches, should in general not be saved in the same location as the programs (which are typically in the /usr/local/usrapps volume), but instead either in long-term research storage space or in the /share volume depending on how long the data will need to be maintained. Compute nodes **DO NOT** have write access to /usr/local/usrapps, so programs running on a compute node  cannot modify any data saved in that volume. 


Available software
******************

The `Software <https://projects.ncsu.edu/hpc/Software/Software.php>`_ page of the HPC website has a list of the staff-supported software packages, and an overview of the rationale for the HPC's emphasis on user-installed and maintained software packages. Note the section called Sponsored Applications includes a subsection called Bioinformatics Tools, with specific instructions on how to request access to bioinformatics software packages installed and maintained by other users but made available for general use. In general, the easiest way to install bioinformatics software on the HPC for your own use (or for use by others in the same research group as you) is to use `Conda <https://projects.ncsu.edu/hpc/Software/Apps.php?app=Conda>`_ to create a virtual environment that contains all the required dependencies and libraries needed for the package to run. Multiple software packages can be installed in the same virtual environment, provided that they are all compatible in terms of their underlying dependencies; Conda has built-in tools to check for compatibility during the process of package installation.

Containers and reproducible research
************************************

Many software tools are now available in Docker containers, which allows the developer to provide all the dependencies and executable programs in an environment that can be run on any computer with appropriate hardware resources. Docker containers require administrative privileges to run, however, and so are not allowed on the HPC. `Singularity <https://sylabs.io/guides/3.4/user-guide/quick_start.html>`_ is a container program developed specifically for use on computing clusters that runs with ordinary user permissions, and is available on the HPC by executing the command::

	module load singularity

Interoperability with Docker was an objective during development of Singularity, so Docker containers can be downloaded from Docker Hub or other online resources and converted to Singularity containers that can run on the HPC. Remember this *must* be done on a login node, because compute nodes don't have Internet access. See `Support for Docker and OCI <https://sylabs.io/guides/3.4/user-guide/singularity_and_docker.html>`_ in the Singularity documentation for more details. 

**IMPORTANT NOTE** the latest version of Singularity is 3.5, while the version installed on the HPC is version 3.4.2. The links above lead to the documentation for v3.4, but an online search for Singularity containers will lead to the latest version of the documentation - take note of the version of documentation that you read, because there may be some functionalities in v3.5 that don't exist in v3.4. 

Cardiff University is developing `An Introduction to Containers and Singularity <https://arcca.github.io/intro_singularity/index.html>`_ - although the site is not yet complete, it already has useful information and guidance. 
	
Setting up a job submission script
**********************************

* Similar to other shell scripts, batch job scripts start by specifying the shell that will process the script, e.g. #!/bin/bash or another shell.
* The next lines specify options for the batch submission process, including details like the number of compute cores required, the amount of time to be allocated to the batch job, the amount of memory needed, the job name, and the output files to which errors and job outputs should be written.
* After all the options are specified, then the code that actually loads software modules and executes the desired programs is included in the script. Depending on the number of different tasks to be executed, there may be a need to load multiple software modules and ensure compatibility among the versions of different software packages to be used in the analysis.


Setting up NCSU AFS and Drive Access
***********************************************
*  `AFS filespace and NCSU Drive <https://oit.ncsu.edu/my-it/filespace/ncsu-drive>`_ filespace are two different storage options that are available to NCSU campus community members (students, staff, and faculty). Access to these storage volumes is enabled on the VCL instances used in class. Access to AFS filespace is enabled by default and a directory called AFS is created in the home directory of each user. The user's AFS storage can also be accessed from Windows or Mac desktop or laptop computers; the OIT webpage linked above has information on how to set up this access. Saving work from the VCL instance to these non-volatile storage options is important if you want keep any files produced during a VCL work session, as all user-created files saved on the virtual machine instance will be lost when the work session is terminated.


Last modified 4 January 2022.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.

