.. _installation_guide:

Installation Guide
==================

.. _`Only for Prediction`:

Only for Prediction
-------------------

DDGWizard mainly consists of two parts: the prediction part, used to predict ΔΔG, and the characterization part, which extracts features from the raw ΔΔG dataset to generate a feature set. If you only need to predict ΔΔG, you just need to install the first part. The installation steps are as follows, which will take about 2 hours.

#. Git clone this repository (replace "Your_Path" with the folder on your local system where you want to install):

    .. code-block:: shell

        cd Your_Path/
        git clone https://github.com/Mingkai14/DDGWizard.git

#. Create conda virtual environment and install conda dependencies:

    .. code-block:: shell

        cd Your_Path/DDGWizard/src/
        vi environment.yml

    You must first modify change the prefix of the environmental.yml file to the path of your local conda envs folder. After modifying, the prefix should be "Your/Conda/Path/envs/DDGWizard".

    .. code-block:: shell

        conda env create -f environment.yml
        conda activate DDGWizard

   Environment description: program was tested on Ubuntu v20.4, conda v23.0, and Python 3.10.2 and require the gcc version of Linux must be greater than 4.8.5.

#. Create your Blast database for sequence alignment:

   You need to download the fasta database file and transfer it to Blast database, allowing program to conduct sequence alignment.

   We tested with uniref50 database and you can download it ("uniref50.fasta.gz") from https://ftp.uniprot.org/pub/databases/uniprot/uniref/uniref50/.

   (The larger database allows more sufficient sequence alignment, but if you want to test the program first, you can download smaller fasta database files, like "uniref2010_01.tar.gz" from https://ftp.uniprot.org/pub/databases/uniprot/previous_releases/release-2010_01/uniref/).

   Once you finish downloading, you need to unzip it:

   .. code-block:: shell

       gzip -d your_fasta_database.gz

   If you are using previous uniref database file, it will be "tar.gz" format:

   .. code-block:: shell

       tar -zxvf your_fasta_database.tar.gz

   You can obtain a fasta file as the raw sequence database file.

   Then you need to use Blast suite to transfer the fasta file to the Blast database. There is an existing blast+ 2.13.0 program folder in our program. Please use the command as follows ("Your_DB_Name" is the name you have assigned to the generated Blast database, which will also be used as a parameter in the DDGWizard):

   .. code-block:: shell

       cd Your_Path/DDGWizard/bin/ncbi_blast_2_13_0+/bin/
       chmod -R +x .
       ./makeblastdb -in Your_Path/your_fasta_database.fasta -dbtype prot -out Your_Path/Your_DB_Name -parse_seqids

   This step will take some time as Blast is building the index to generate the sequence database. The duration depends on the size of the database file you have selected and the performance of your computer.

#. Configure Modeller:

   Modeller is used to generate mutation structures, it was already installed when creating conda environment. But it also need a license.

   You need to enter in Modeller official website to register an account and get the license, from https://salilab.org/modeller/registration.html. Then modify Modeller conda config file to add license:

   Open your Modeller conda config file, which should be in "Your_Conda_Path/envs/DDGWizard/lib/modeller-10.4/modlib/modeller/config.py" and replace the XXXX in "config.py" file to your license. After modifying, save and close it.

#. Configure DSSP:

   DSSP is used to calculate the RSA (relative surface area) and secondary stuctures.
   Due to version conflict issues, you must do operations below to make DSSP can be used:

   .. code-block:: shell

       conda activate DDGWizard
       whereis mkdssp

   You will obtain the location of mkdssp (a modified version of dssp), recording the directory path where mkdssp is located as "the_directory_of_mkdssp" (should be "Your/Conda/Path/envs/DDGWizard/bin/"):

   .. code-block:: shell

       cd the_directory_of_mkdssp
       cp mkdssp dssp

#. Last step: make sure the files of the DDGWizar have the executable permission:

   You must perform this step, otherwise the program will not function properly:

   .. code-block:: shell

       cd Your_Path/DDGWizard
       chmod -R +x .

.. _`Both for Prediction and Characterization`:

Both for Prediction and Characterization
----------------------------------------

If you need to characterize the raw ΔΔG data, extracting features from its PDB files or sequences for analysis or machine learning purposes, you can use DDGWizard's characterization part. The characterization part requires additional installations to calculate the complete feature set, and for cross-platform calling certain software to calculate, DDGWizard uses Singularity to automatically call corresponding software within the container.

#. Complete steps 1-6 identical to the prediction part:

   Perform the same operations as steps 1-6 in the prediction part.

#. Configure R:

   You need to install R and R package "Bio3D"::

    (How to install R?)
    R
    install.packages("bio3d")

#. Configure container evironment:

   Characterization part also runs some software in specific linux system. To solve platform compatibility, we use container to run these software. Our script will automatically call commands to run container. Docker and Singularity are supported. You only need to configure one of both.

   There are two were supported? If you want to use Docker:
   You need to follow docker official instructions to install docker (?).
   You must add your user to docker super privilege user group, which should have set when docker was installed::

    sudo usermod -aG docker Your_User_Name
    (Then restart your linux system)

   You need to load docker image from software folder::

    docker load -i Your_Path/DDGWizard/src/Prof_Source/myprof.tar

   If you want to use Singularity:
   (only install singularity, how? download big file)
   You need to follow singularity official instructions to install singularity. You don't need to additionally configure using singularity.

#. Make sure all files have run permission::

    cd Your_Path/DDGWizard
    chmod -R +x .




