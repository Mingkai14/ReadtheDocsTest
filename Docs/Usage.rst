.. _usage:

.. raw:: html

    <style>.highlight {
            background-color: #E7FC9F;
            color: #000000;
            padding: 6px;
            font-size: 12px;
            font-weight: 100;
        }
            .keyword-highlight {
            background-color: #FFFFF0;
            color: #FF3366;
            padding: 6px;
            font-size: 12px;
            font-weight: 100;
        }
    </style>

Usage
========

.. _`Predict ΔΔG`:

Predict ΔΔG
-------------------------

.. raw:: html

    <div style="text-align: justify;">
    This guide is intended to show users who aim to characterize raw ΔΔG data. It will output complete ΔΔG feature set for analysis or machine learning purposes.
    <p></p>
    The characterization part requires additional prerequisites to meet the needs of calculation for complete feature set. The characterization part uses certain R-based packages and certain cross-platform software, thus requiring dependencies on the R language and the container system.
    <p></p>
    <h4>Additional prerequisites:</h4>
    R; Docker or Singularity (Only one is needed).
    <p></p>
    </div>

   This python program aims to predict ddG.

#. an example:
   You can run program Like::

    conda activate DDGWizard
    cd Your_Path/DDGWizard/
    python Predict_ddG_Executable.py
     --pred_dataset_path your_dataset.xls
     --db_folder_path Your_Path/blast_db_folder/
     --db_name db_name
     --if_reversed_data 0
     --blast_process_num 4
     --mode whole
     --process_num 4  (Line break issue)

#. Arguments:

   (1). --pred_dataset_path:

        Provide a xls file path, the file include data you want to predict.

        File must be xls format and it has several attributes (examples?explain)::

            Name (Identify this protein with a name consisting of fewer than 8 characters, and duplication is allowed but one name must only correspond to one pdb file)

            PDB_File_Path (The file path of the PDB protein that you need to predict. This must be an absolute path.)

            Variation (Specify the mutated amino acid, the mutation site number consistent with the PDB file, and the desired mutated amino acid. like: Y57H)

            Chain (Specify the chain number mutated amino acid located, consistent with the PDB file)

            pH (Specify pH)

            T (Specify temperature)

            (Do not include complete same data in your xls file.)


        There is an examples?explain?

        +-------------+---------------------+------------------+----------------+----------+------------------+
        | Name        | PDB_File_Path       | Variation        | Chain          |   pH     |  T               |
        +=============+=====================+==================+================+==========+==================+
        | 1SHG        | /.../.../1SHG.pdb   | Y57H             |   A            |   7      |  24.8            |
        +-------------+---------------------+------------------+----------------+----------+------------------+
        | 1SHG        | /.../.../1SHG.pdb   | A56E             |   A            |  3.2     |  54              |
        +-------------+---------------------+------------------+----------------+----------+------------------+
        | 2AFG        | /.../.../2AFG.pdb   | C117I            |   A            |  6.6     |  25              |
        +-------------+---------------------+------------------+----------------+----------+------------------+

        There is a sample file in Your_Path/DDGWizard/src/sample_pred.xls
        (If you want to perform predictions for saturation mutagenesis or full-site saturation mutagenesis, we recommend using our provided utility_tool.py script.)

   (2). --db_folder_path:
       Provide folder path of your blast database.

   (3). --db_name:
       Provide your blast database name.

   (4). --if_reversed_data:
       Provide 0 or 1, indicate if you also want to predict reverse mutations.

   (5). --blast_process_num:
       Provide a number less than 200 and greater than 0. DDGWizard will run blast in multi-process.

   (6). --mode:
       Default is "whole". DDGWizard will run complete processes. "model_only" mean only generate mutation structures. "blast_only" mean only run blast. When there is a large amount of data to be processed, this mechanism allows the task to be completed in segments.

   (7). --process_num:
       Provide a number less than 200 and greater than 0. DDGWizard will calculate data in multi-process.

#. Output:

   There will be a output xls file in Your_Path/DDGWizard/Pred_Res/, recording all prediction results.

.. _`Generate_Dataset_Executable.py`:

Generate_Dataset_Executable.py
------------------------------

   This python program aims to extract features from raw data. Its generation of 1547 features can assist protein thermodynamic characterization and prediction related with protein thermodynamics.

#. an example:
   You can run program Like::

       conda activate DDGWizard
       cd Your_Path/DDGWizard/
       python Generate_Dataset_Executable.py
       --raw_dataset_path Your_Raw_Dataset/dataset.xls
       --db_folder_path Your_Path/blast_db_folder/
       --db_name db_name
       --if_reversed_data 1
       --blast_process_num 4
       --container_type D
       --mode whole
       --process_num 4

#. Arguments:

   (1). --raw_dataset_path:
       Provide your raw data path. It must save as xls format. The first row must have these attributes::

        PDB, Variation, Chain, ddG, pH, T (color?)

       A sample file is in Your_Path/DDGWizard/src/sample.xls.

   (2). --db_folder_path:
       Provide folder path of your blast database.

   (3). --db_name:
       Provide your blast database name.

   (4). --if_reversed_data:
       Provide 0 or 1, indicate if you want to generate features of reverse mutations.

   (5). --blast_process_num:
       Provide a number less than 200 and greater than 0. DDGWizard will calculate data in multi-process.

   (6). --container_type:
       "D" means use docker, "S" means use singularity.

   (7). --mode:
       "model_only" mean only generate mutation models, "blast_only" mean only generate blast output files, "whole" mean completely process.

   (8). --process_num:
       Provide a number less than 200 and greater than 0. DDGWizard will calculate data in multi-process.

#. Output:
   After running, it will generate a csv file name features_table.csv in Your_Path/DDGWizard/src/Features_Table/

.. _`utility_tool.py`:

utility_tool.py
---------------

   (why?what?how)This script assists userss with prediction requirements of saturation mutagenesis and full-site saturation mutagenesis in quickly preparing input files. After?

#. examples:

   For saturation mutagenesis (?), it will prepare data for the remaining 19 possible amino acid mutations based on the chain, site number, and wild-type amino acid you input, for next prediction::

       python utility_tool.py
       --pdb_name Your_PDB_Name
       --pdb_path Your_PDB_Path
       --chain chain_site_located
       --site_number site_located_consistent_with_PDB_file
       --wt_aa Wild_Type_amino_acid
       --pH Your_pH
       --T Your_Temperature

   For full-site saturation mutagenesis (?), you don't need to input the chain and wild-type amino acid. Just type 'all' in the site number parameter, and it will prepare all possible mutation data for all sites across all chains::

       python utility_tool.py
       --pdb_name Your_PDB_Name
       --pdb_path Your_PDB_Path
       --site_number all
       --pH Your_pH
       --T Your_Temperature

#. Arguments:

   ?

#. Output:

   It will generate pred.xls (what?) in ./src/ including whole data wait to predict.

   Then you can directly use like? to run, like::

       cd ?
       python Predict_ddG_Executable.py
       --pred_dataset_path ./src/pred.xls
       --db_folder_path Your_Path/blast_db_folder/ --db_name your_db_name --if_reversed_data 0 --blast_process_num 4 --mode whole --process_num 4' to perform the prediction.









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

.. _`Tips`:

Tips
-------------------

   (1). You must cd to the top folder of DDGWizard to run and make sure you are in DDGWizard virtual environment and finish environment preparation.

   (2). DDGWizard itself supports multiprocessing. We recommend utilizing our built-in multiprocessing fuction. Avoid running multiple DDGWizard in the same time and in the same folder, as conflicts may arise when the program matches files. If you genuinely need to implement multiprocessing or multithreading for running DDGWizard by yourself, please make copies of the DDGWizard folder. Ensure that each instance of the DDGWizard program running in different processes/threads resides in a separate folder.

   (3). Avoid to place your files, such as data files, in the top folder of DDGWizard. The program will automatically clean up files in the top folder that are unrelated to the program. It is recommended to place them in ./src/
