# Data and code for analysis for "Evidence from Drosophila supports higher duplicability of faster evolving genes."

This repository contains the required code and data to produce results presented in (REF). Additional software used:

=========================================================================================================
##Miscellaneous

** Analysis_code.ipynb: ** Python code including data processing, statistical analysis and figure production
** drosophilaProjectNcbiFtpFileLocations: ** locations of genome annotations used on the NCBI FTP site
speciesAbbrevs.txt: species names corresponding to the abbreviations used across the analysis
drosophilaDatabase_diptera: database containing all genes which were considered singletons for input into the data filtering pipeline
Columns:

===========================================================================================================================
#Sequence data

dipteraCDS_raw: .fasta files containing CDS sequences for each species, as downloaded

dipteraTranslations_raw: .fasta files containing translated CDS sequences for each species, as downloaded

dipteraTranslations_processed: processed .fasta files containing translated CDS sequences for each species, longest sequence for each gene only. Headers are formatted: gene|protein|species


=========================================================================================================
Figures : .png versions of figures included in (REF)

=========================================================================================================

Fast-evolving singletons: Output files relating to analysis of the impact of faster rate of evolution on duplicate detection

=========================================================================================================
