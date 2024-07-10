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
    To meet this practical user's need, we have prepared a program to help users quickly generate an <span class="keyword-highlight">XLS</span> file of saturation mutagenesis. This file serves as input for DDGWizard to predict the ΔΔG of saturation mutagenesis.
    <p></p>
    </div>

.. raw:: html

    <div style="text-align: justify;">
    <h4>1. Example of running</h4>
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
