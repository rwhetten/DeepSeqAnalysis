.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash


HPC and LSF
===========


Objective
*********

The objective of this section is to work through NCSU's High-Performance Cluster (HPC) quick-start tutorial to gain familiarity with the NC State HPC, and use other reference videos to review and practice cluster job submission using LSF. `Singularity containers <https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0177459>`_ are an important asset for working on the HPC, because they allow preservation of exactly the same working environment for the duration of a project, and can be made available to other scientists in pursuit of the goal of reproducible research. Unlike Docker containers, which require root access to run, Singularity containers run with the same permissions of the user who launches the container, but can still be deployed on computing clusters to take advantage of the hardware resources available there.    


Exercises
*********

Using NC State University's High-Performance Computing (HPC) Service:

1. Go to the `quick-start guide <https://projects.ncsu.edu/hpc/Guide/index.php>`_ page on the HPC website.

2. Either watch and follow along with the `video guide <https://youtu.be/RXKzN3osLR8>`_ or work through the text version at the bottom of the same page.

3. A Zoom video recording of the class session working through the Quick-Start tutorial is available `with this link <https://ncsu.zoom.us/rec/play/upUqJOCpqG03HtKRtQSDAPB-W47oLqys1yMbrPUNzhnnUXILNQelb7NEYuAksjKwuIdXu_z0x_k4IH92?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=1mdUOXF80CeAm345lh6PIvftUuOV_Q-Jf>`_ & `transcript download <https://drive.google.com/open?id=1Y-DchMpqrMNv58Z03i-SRnrIZVhgb6eD>`_)

4. A `text file <https://drive.google.com/open?id=15_RzI6yQqB-BRUVYl70y6AucvhI8EfZQFbC64mUYJEU>`_ is available with an overview of commands used to set up a Conda environment on the HPC, and an example LSF job script used to carry out a series of commands using software installed through Conda. A Zoom video recording of the class session working through conda setup and LSF job submisson is available `with this link <https://ncsu.zoom.us/rec/play/uZZ-I7ihrmk3EoDDtgSDB_YtW461JqOs0nMd_KcFzx3hBndWYFf3NLVAYyzsdId1nlkPrQ2X1vQU9-c?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=19CTrmUv27c_upafnUEj2Y0g2kXKJdWzV>`_ & `transcript download <https://drive.google.com/open?id=1cXAYhbLFLma6ZSeRBQ1zm6dlyXa0d6g->`_).

5. A `text file <https://docs.google.com/document/d/1OIVhHsFscXNezba3KHaWEZ7svNq_jYotB9l3mvidfNA>`_ is available with an outline of steps required to set up a Conda environment with Trinity and Transdecoder, do de novo transcriptome assembly, and carry out functional annotation. Sorting out the details of how to do these steps is left as an exercise. A Zoom video recording of the class session working through these steps is available `with this link <https://ncsu.zoom.us/rec/play/uJModu75r2k3TNGV4QSDB_ItW43pK_-s0ihN-PANmk22WnlQNlf3YLYba-VII4xxRXa2x5abeHm2I9W-?continueMode=true>`_ (or `by video download <https://drive.google.com/open?id=1n017W53zp8ZoMc3arG7BW5z1IGwbgCWQ>`_ & `transcript download <https://drive.google.com/open?id=1WSk6MLEDpl0bfEKzsPSc_mzxq36v2kNV>`_).

Resources
*********

`NCSU OIT HPC main page <https://projects.ncsu.edu/hpc/main.php>`_

`NCSU HPC LSF guide <https://projects.ncsu.edu/hpc/Documents/LSF.php>`_

`NCSU HPC conda guide <https://projects.ncsu.edu/hpc/Software/Apps.php?app=Conda>`_ - Conda is the preferred method for installing software on the HPC, because it provides a way to manage dependencies and version requirements. Conda was originally written primarily for managing Python virtual environments, but has been extended to include a variety of software not related to Python. See the `Bioconda site <https://bioconda.github.io/>`_ for more information about the enormous variety (> 7000 different bioinformatics programs) available for installation through the bioconda channel of Conda.

`NCSU Bioinformatic Users Group (deBUG) <https://ncsu-debug.readthedocs.io/en/latest/#>`_ ReadtheDoc site.

`Singularity v3.5 documentation <https://sylabs.io/guides/3.5/user-guide/>`_ from Sylabs.io

`Using Singularity on the NIH HPC <https://hpc.nih.gov/apps/singularity.html>`_ is documentation for the NIH cluster, but has lots of useful advice and links with more information

`Using Singularity on the NC State BRC cluster <https://brcwebportal.cos.ncsu.edu/cluster_workshop/doku.php?id=using_singularity>`_ is specific to the BRC cluster, which uses SLURM rather than LSF. This also has good advice and links.

Last modified 9 April 2020.
Edits by `Ross Whetten <https://github.com/rwhetten>`_ and `Will Kohlway <https://github.com/wkohlway>`_.
