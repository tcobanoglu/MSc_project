This zip archive contains the code necessary for
runing the InKA pipe-line as presented in :

"INKA, an integrative data analysis pipeline for 
phosphoproteomic inference of active kinases", 
Robin Beekhof et al. 

Algorithm is free exclusively for academic use. If used 
in publication, please cite.


Description for using the InKA pipe-line
========================================

The InKA pipeline consists of the following 
essential components:

1) read_MQ_tables.R
2) inka.R
3) collect_output_tables.R

4) complete-HGNC-21Apr2016.csv
5) Kinases_HGNC2017.01.20_v2.Rdata
6) phomics_global_output.txt
7) PSP_human_03Jul2016.Rdata
8) PSP_KSR_human_03Jul2016.Rdata
9) TOP_NWK_nwk_proteome_unprot_ref_2014.Rdata
10) UniProt_data_08Jun2016.Rdata

and these additional files

11) make_intensity_pp.R
12) example_data.zip
13) README.txt

Running InKA 
============

The following R packages are sufficient for running InKA:

data.table      >= 1.11.4
stringr         >= 1.3.1
splitstackshape >= 1.4.6
network         >= 1.13.0.1

The easiest way of running InKA is by extracting from the
archive example_data.zip the required input files from a 
suitable MaxQuant phospho search, into this code directory:

evidence.txt
experimentalDesignTemplate.txt
modificationSpecificPeptides.txt
Phospho (STY)Sites.txt

Followed by execution of the scripts

./read_MQ_tables.R
./inka.R

directly from the command-line or an R prompt.

This will create amongst others a file called "inka_out.pdf" 
containing the output of the analysis.

The script

./collect_output_tables.R

can be called to construct tables containing the InKA
scores for all kinases in all samples, and corresponding tables
for each of the submetrics that used in the construction of the InKA 
score.

For phosphorylated tyrosine IP derived data, we recommend using the 
scripts as shown above. For TiOx and other non-exclusively phospho 
tyrosine enriched samples, using 

./inka.R --tiox

might improve result presentation and also run much faster, as 
for serine/threonine phosphorylation both size and KS-relation volume 
can be considerably larger.

A second utility script

make_intensity_pp.R

is provided to be run in the following command sequence

./read_MQ_tables.R
./make_intensity_pp.R
mv pp-Peptide-report_intensities.txt  pp-Peptide-report.txt
./inka.R

resulting in an MS1 signal intensity-based InKA analysis.

Additional flags recognized by the inka.R script are

./inka.R --no.network 

which wiil supress the kinase substrate network generation
in the output.

Additional information
======================

Note that the above description assumes that the files

collect_output_tables.R
inka.R
read_MQ_tables.R
make_intensity_pp.R

are executable (Execute "chmod +x *.R evquant" if this is not the case).

