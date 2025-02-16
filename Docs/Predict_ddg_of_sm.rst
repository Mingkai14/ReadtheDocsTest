.. _Predict ΔΔG of saturation mutagenesis:

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

Predict ΔΔG of saturation mutagenesis
======================================

.. raw:: html

    <div style="text-align: justify;">
    This guide is intended to show users how to quickly use DDGWizard to predict ΔΔG of saturated mutations.
    <p></p>
    Saturation mutagenesis represents mutating the original amino acid residue at the same mutation site to all possible amino acids. In practical applications, users often require predicting the ΔΔG of saturation mutagenesis at one or all amino acid sites, thereby assessing which mutations may enhance thermostability of the protein based on a wide range of possibilities.
    <p></p>
    To meet this practical user's need, we have prepared a program to help users quickly generate the needed <span class="keyword-highlight">xls</span> file of saturation mutagenesis. This file serves as input for DDGWizard to predict the ΔΔG of saturation mutagenesis.
    <p></p>
    </div>

.. raw:: html

    <div style="text-align: justify;">
    <h4>1. Example template</h4>
    <p>Similarly, we first provide two examples of running this program, followed by a detailed explanation of the program parameters. We selected the protein <span class="keyword-highlight">1SHG</span> from <span class="keyword-highlight">DDGWizard/src/pdbs/</span> as a case study.</p>
    <p></p>
    If you want to predict the ΔΔG of saturation mutagenesis at a single site, you can run the program with:
    <p></p>
    <div>

.. raw:: html

    <div class="highlight-default notranslate">
    <div class="highlight">
    <pre style="overflow: scroll">
    $ conda activate DDGWizard
    $ cd DDGWizard/
    $ python utility_tool.py \
       --pdb_name 1SHG \
       --pdb_path ./src/pdbs/1shg.pdb \
       --chain A \
       --site_number 57 \
       --wt_aa Y \
       --pH 7 \
       --T 25
    </pre>
    </div>
    </div>


.. raw:: html

    <div style="text-align: justify;">
    <h4>1. Example of running</h4>
    <p>Similarly, we first provide two examples of running this program, followed by a detailed explanation of the program parameters. We selected the protein <span class="keyword-highlight">1SHG</span> from <span class="keyword-highlight">DDGWizard/src/pdbs/</span> as a case study.</p>
    <p></p>
    If you want to predict the ΔΔG of full-site saturation mutagenesis, you can run the program with:
    <p></p>
    <div>

.. raw:: html

    <div class="highlight-default notranslate">
    <div class="highlight">
    <pre style="overflow: scroll">
    $ conda activate DDGWizard
    $ cd DDGWizard/
    $ python utility_tool.py \
       --pdb_name 1SHG \
       --pdb_path ./src/pdbs/1shg.pdb \
       --site_number all \
       --pH 7 \
       --T 25
    </pre>
    </div>
    </div>

.. raw:: html

    <div style="text-align: justify;">
    <h4>2. Parameter details</h4>
    Below are the details of the parameters for the program of saturation mutagenesis:
    <p></p>
    (1). <span class="keyword-highlight">----pdb_name</span>
    <p></p>
    This parameter indicates that you need to provide a name to label the predicted protein. It corresponds the <span class="keyword-highlight">Name</span> attribute of generated <span class="keyword-highlight">xls</span> file.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (2). <span class="keyword-highlight">----pdb_path</span>
    <p></p>
    This parameter indicates that you need to provide a path to the <span class="keyword-highlight">PDB</span> file of the predicted protein. It corresponds the <span class="keyword-highlight">PDB_File_Path</span> attribute of generated <span class="keyword-highlight">xls</span> file.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (3). <span class="keyword-highlight">--chain</span>
    <p></p>
    This parameter indicates that you need to provide the chain identifier of the protein where the predicted mutation are located. It corresponds the <span class="keyword-highlight">Chain</span> attribute of generated <span class="keyword-highlight">xls</span> file.
    <p></p>
    If you intend to predict the ΔΔG of full-site saturation mutagenesis and the parameter <span class="keyword-highlight">--site_number</span> was provided with the value <span class="keyword-highlight">all</span>, you don't need to provide this parameter. The program will automatically match the chain identifier for all possible mutations.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (4). <span class="keyword-highlight">--site_number</span>
    <p></p>
    This parameter indicates that you need to provide the site number of the predicted mutation.
    <p></p>
    If you intend to predict the ΔΔG of full-site saturation mutagenesis, please provide the value <span class="keyword-highlight">all</span>.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (5). <span class="keyword-highlight">--wt_aa</span>
    <p></p>
    This parameter indicates that you need to provide the wild-type amino acid of the predicted mutation.
    <p></p>
    If you intend to predict the ΔΔG of full-site saturation mutagenesis and the parameter <span class="keyword-highlight">--site_number</span> was provided with the value <span class="keyword-highlight">all</span>, you don't need to provide this parameter. The program will automatically match the wild-type amino acid for all possible mutations.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (6). <span class="keyword-highlight">--pH</span>
    <p></p>
    This parameter indicates that you need to specify at which pH you want to predict the ΔΔG for the mutations. It corresponds the <span class="keyword-highlight">pH</span> attribute of generated <span class="keyword-highlight">xls</span> file.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    (7). <span class="keyword-highlight">--T</span>
    <p></p>
    This parameter indicates that you need to specify at which temperature you want to predict the ΔΔG for the mutations. It corresponds the <span class="keyword-highlight">T</span> attribute of generated <span class="keyword-highlight">xls</span> file.
    <p></p>
    <div>

.. raw:: html

    <div style="text-align: justify;">
    <h4>3. Output</h4>
    The program will generate an output xls file <span class="keyword-highlight">pred.xls</span> located in <span class="keyword-highlight">DDGWizard/src/</span>.
    <p></p>
    This <span class="keyword-highlight">xls</span> file can be directly used as input for the DDGWizard prediction program, enabling quick preparation for ΔΔG prediction of saturation mutagenesis:
    <p></p>
    </div>

.. raw:: html

    <div class="highlight-default notranslate">
    <div class="highlight">
    <pre style="overflow: scroll">
    $ conda activate DDGWizard
    $ cd DDGWizard/
    $ python Predict_ddG_Executable.py \
        --pred_dataset_path ./src/pred.xls \
        --db_folder_path <b>&lt;the path to save Blast database&gt;</b> \
        --db_name <b>&lt;the name to assign for Blast database&gt;</b> \
        --if_reversed_data 0 \
        --blast_process_num 4 \
        --mode whole \
        --process_num 4
    </pre>
    </div>
    </div>

.. raw:: html

    <div style="text-align: justify;">
    1. adding tips 2. finish sm 3. finish generate 3.1. supplement container of install 4. overall optimize 5. test by yourself
    </div>
