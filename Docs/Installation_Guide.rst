.. _installation_guide:

Installation Guide
==================

.. _`Only for Prediction`:

Only for Prediction
-------------------

#. Git clone this repository::

    cd Your_Path/
    git clone https://github.com/Mingkai14/DDGWizard.git

#. Create conda virtual environment and install conda dependencies::

    cd Your_Path/DDGWizard/src/
    vi environment.yml
    (Change prefix in environment.yml to your own location of conda envs folder (/Your/Conda/Path/envs/DDGWizard).
    conda env create -f environment.yml
    conda activate DDGWizard

   Conda yml file in Your_Path/DDGWizard/src/environment.yml; Your gcc version must be greater than 4.8.5 and conda version must be greater than 23.0.

#. Create your Blast database:

You need to prepare your own Blast database.

You need to download fasta database file first. We used uniref50.fasta file (you can download from `uniref_db`).

We recommend you use blast+ 2.13.0 version. And there is an existing blast+ program folder in our program. Recommend you directly use this::

    cd Your_Path/DDGWizard/bin/ncbi_blast_2_13_0+/bin/
    chmod -R +x .
    ./makeblastdb -in Your_Path/uniref50.fasta -dbtype prot -out Your_Path/Your_DB_Name -parse_seqids

#. Configure Modeller:

Modeller was used to generate mutation structures, it was already installed by conda. But it also need a license.

.. _`Both for Prediction and Characterization`:

Both for Prediction and Characterization
----------------------------------------

.. _uniref_db: https://ftp.uniprot.org/pub/databases/uniprot/uniref/


