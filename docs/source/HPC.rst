.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


HPC and LSF
===========


Objective
*********

The objective of this section is to work through NCSU's High-Performance Cluster (HPC) quick-start tutorial to gain familiarity with the NC State HPC, and use other reference videos to review and practice cluster job submission using LSF, the job management system of the HPC. `Singularity containers <https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0177459>`_ are an important asset for working on the HPC, because they allow preservation of exactly the same working environment for the duration of a project, and can be made available to other scientists in pursuit of the goal of reproducible research. Unlike Docker containers, which require root access to run, Singularity containers run with the same permissions of the user who launches the container, but can still be deployed on computing clusters to take advantage of the hardware resources available there. Access to the NC State HPC is available to faculty, staff and students at NC State University - see `Request Access <https://projects.ncsu.edu/hpc/Accounts/GetAccess.php>`_ for more information. Mac and Linux users can connect directly to the HPC by SSH to login.hpc.ncsu.edu from a terminal window; Windows users should install `MobaXterm <https://mobaxterm.mobatek.net/download.html>`_ to provide a terminal environment for SSH as well as a number of other useful tools. The HPC uses a tool called Load Sharing Facility (LSF) to manage the queues of computing jobs submitted for processing on the HPC - see the `LSF Document <https://projects.ncsu.edu/hpc/Documents/LSF.php>`_ for more information about LSF scripts.  


Exercises
*********

Using NC State University's High-Performance Computing (HPC) Service:

1. Go to the `quick-start guide <https://projects.ncsu.edu/hpc/Guide/index.php>`_ page on the HPC website.

2. Either watch and follow along with the `video guide <https://youtu.be/RXKzN3osLR8>`_ or work through the text version at the bottom of the same page.

3. A Zoom video recording of the class session working through the Quick-Start tutorial is available `with this link <https://ncsu.zoom.us/rec/play/upUqJOCpqG03HtKRtQSDAPB-W47oLqys1yMbrPUNzhnnUXILNQelb7NEYuAksjKwuIdXu_z0x_k4IH92?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=1mdUOXF80CeAm345lh6PIvftUuOV_Q-Jf>`_ & `transcript download <https://drive.google.com/open?id=1Y-DchMpqrMNv58Z03i-SRnrIZVhgb6eD>`_)

4. A `text file <https://drive.google.com/open?id=15_RzI6yQqB-BRUVYl70y6AucvhI8EfZQFbC64mUYJEU>`_ is available with an overview of commands used to set up a Conda environment on the HPC, and an example LSF job script used to carry out a series of commands using software installed through Conda. A Zoom video recording of the class session working through conda setup and LSF job submisson is available `with this link <https://ncsu.zoom.us/rec/play/uZZ-I7ihrmk3EoDDtgSDB_YtW461JqOs0nMd_KcFzx3hBndWYFf3NLVAYyzsdId1nlkPrQ2X1vQU9-c?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=19CTrmUv27c_upafnUEj2Y0g2kXKJdWzV>`_ & `transcript download <https://drive.google.com/open?id=1cXAYhbLFLma6ZSeRBQ1zm6dlyXa0d6g->`_).

5. A `text file <https://docs.google.com/document/d/1OIVhHsFscXNezba3KHaWEZ7svNq_jYotB9l3mvidfNA>`_ is available with an outline of steps required to set up a Conda environment with Trinity and Transdecoder, do de novo transcriptome assembly, and carry out functional annotation. Sorting out the details of how to do these steps is left as an exercise. A Zoom video recording of the class session working through these steps is available `with this link <https://ncsu.zoom.us/rec/play/uJModu75r2k3TNGV4QSDB_ItW43pK_-s0ihN-PANmk22WnlQNlf3YLYba-VII4xxRXa2x5abeHm2I9W-?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=1n017W53zp8ZoMc3arG7BW5z1IGwbgCWQ>`_ & `transcript download <https://drive.google.com/open?id=1WSk6MLEDpl0bfEKzsPSc_mzxq36v2kNV>`_).

6. `Notes from 10 April 2020 <https://docs.google.com/document/d/12MuVvPPCjbdK6mJHD5wMrBjmygx2ezm6RoaHB4yaXag>`_ - an exercise to carry out assembly and annotation of a yeast RNA-seq dataset using Trinity, TransDecoder, and Trinotate installed in a Conda environment.

Final Project
*************

The Final Project is optional, but highly recommended to complete. The goal of this project (should you choose to accept it), is to utilize the HPC and LSF scripting to.. 


1. Do a de novo transcriptome assembly with yeast RNA-seq data.

2. Identify open reading frames, and annotate those ORFs using results of protein similarity searches, protein domain analysis, and various other tools. 


The software to be used includes the Trinity assembler, the TransDecoder suite for identification of ORFs, and the Trinotate suite for annotation. You will need to install the necessary tools to a Conda environment on the HPC. The text file linked to the HPC and LSF section under section 6 of Exercises has some notes on how to set up and run the Conda environment to carry out the Trinity assembly as an example. The diamond (protein similarity search) and Pfam (protein domain search) databases are available at /share/bit815s20/databases. The RNA-seq data are in /share/bit815s20/yeast/RNAdata - look for the six files [rnaC1, rnaC2, rnaC3][_1.fastq.gz,_2.fastq.gz]. The TransDecoder and Trinotate pipelines will be similar, but (of course) using commands specific to those software packages.

More detailed information on how to structure the commands for Trinity, TransDecoder, and Trinotate is available at the respective websites for those software packages. The ability to find the information you need to understand how to use software is an important skill to practice, as new software and new methods emerge all the time. However, we are available to answer questions, either via the Slack channel or during class meetings.



Resources
*********

`NCSU OIT HPC main page <https://projects.ncsu.edu/hpc/main.php>`_

`NCSU HPC LSF guide <https://projects.ncsu.edu/hpc/Documents/LSF.php>`_

`NCSU HPC conda guide <https://projects.ncsu.edu/hpc/Software/Apps.php?app=Conda>`_ - Conda is the preferred method for installing software on the HPC, because it provides a way to manage dependencies and version requirements. Conda was originally written primarily for managing Python virtual environments, but has been extended to include a variety of software not related to Python. See the `Bioconda site <https://bioconda.github.io/>`_ for more information about the enormous variety (> 7000 different bioinformatics programs) available for installation through the bioconda channel of Conda.

`NCSU Bioinformatic Users Group (deBUG) <https://ncsu-debug.readthedocs.io/en/latest/#>`_ ReadtheDoc site.

`Singularity v3.5 documentation <https://sylabs.io/guides/3.5/user-guide/>`_ from Sylabs.io

`Using Singularity on the NIH HPC <https://hpc.nih.gov/apps/singularity.html>`_ is documentation for the NIH cluster, but has lots of useful advice and links with more information

`Using Singularity on the NC State BRC cluster <https://brcwebportal.cos.ncsu.edu/cluster_workshop/doku.php?id=using_singularity>`_ is specific to the BRC cluster, which uses SLURM rather than LSF. This also has good advice and links.



Class Recordings
----------------

+   `Session 25: recorded March 22nd 2021 <https://drive.google.com/file/d/1h4cCZVNWg8HoySRCnNv08eAcFM6hRIYv/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1zpNSlXdMBVgRj9Ek6Uc--E9Md_LlBopv/view?usp=sharing>`_.
+   `Session 26: recorded March 26th 2021 <https://drive.google.com/file/d/19O_5BsQ3_WLJKasuKTFLaH-rOoy1cecU/view?usp=sharing>`_. 
+   `Session 27: recorded March 29th 2021 <https://drive.google.com/file/d/1H1aF_bPJrNtCiUYSOf2C_jS1KebFzLiD/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1k2M3ULhEYeJxLpjEVCKUsc3-NdxapW2l/view?usp=sharing>`_.
+   `Session 28: recorded March 31st 2021 <https://drive.google.com/file/d/1UR0KqRDp1lSj8RkJSB09cLqeKBULdER_/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1Y-vj0StT-3BuBsg7fHfAMjqlnstamRZd/view?usp=sharing>`_.
+   `Session 30: recorded April 5th 2021 <https://drive.google.com/file/d/189y0H8Ta9QNUGQY25Mg3FVz03ZcP2c68/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/19ysg6ZcXxwUrnhc-Jj61PZOIxpHp_m8U/view?usp=sharing>`_.
+   `Session 31: recorded April 7th 2021 <https://drive.google.com/file/d/1CpLV0miX40Yay_yiuUWwqBlEU5NOrDaw/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1h29BOmaW9SUL-x_krRYetQlI-IroYXJK/view?usp=sharing>`_.
+   `Session 32: recorded April 8th 2021 <https://drive.google.com/file/d/1ugrRnCMCD-sBI_DP1gthSCGHAh6KVs8s/view?usp=sharing>`_. A trancscript of the recording is `also availabile <https://drive.google.com/file/d/1lpmnb_FloOWYoWFBVkeJNMQsI8ebQ81W/view?usp=sharing>`_.


Last modified 4 January 2022.
Edits by `Ross Whetten <https://github.com/rwhetten>`_ and `Will Kohlway <https://github.com/wkohlway>`_.
