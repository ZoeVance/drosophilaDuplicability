# Data and code for analysis for "Evidence from Drosophila supports higher duplicability of faster evolving genes."

This repository contains the required code and data to produce results presented in (REF). Additional software used:
* [BLAST+ (v2.11)](https://www.ncbi.nlm.nih.gov/books/NBK279690/)
* [MUSCLE (v3.8)](https://drive5.com/muscle/downloads_v3.htm)
* [IQ-TREE (v1.6.12)](http://www.iqtree.org/)
* [Orthofinder (v 2.5.4)](https://github.com/davidemms/OrthoFinder)
* [SonicParanoid (v1.3.5)](http://iwasakilab.k.u-tokyo.ac.jp/sonicparanoid/)
* [OMA (v2.5)](https://omabrowser.org/standalone/)
* [PAML (v4.9)](http://abacus.gene.ucl.ac.uk/software/paml.html)
* [STAR (v2.7.7a)](https://github.com/alexdobin/STAR/releases)
* [RSEM (v1.3.3)](https://deweylab.github.io/RSEM/)
* [abSENSE](https://github.com/caraweisman/abSENSE)

=========================================================================================================
## Miscellaneous

**Analysis_code.ipynb:** Python code including data processing, statistical analysis and figure production

**drosophilaProjectNcbiFtpFileLocations:** locations of genome annotations used on the NCBI FTP site

**speciesAbbrevs.txt:** species names corresponding to the abbreviations used across the analysis

**dsuz\_all\_genes:** List of all _D.suzukii_ genes included, id format as in .fasta files in dipteraTranslations_processed/

**dsuz\*.out:** BLAST output, 'filtered' file  has been filtered to only include hits with E-value under 0.1, filtered.relaxed to only include hits with E-value under 0.0001

**dsuz_singletons\*.txt:** Starting list of singletons based on BLAST output, 'relaxed' file is based on dsuz.filtered.relaxed.out

**dSuz_exp.genes.results:** Output from RSEM for _D. suzukii_

**drosophilaDatabase_diptera_final.sql:** SQL file to generate a database containing all genes which were considered singletons for input into the data filtering pipeline as well as inferred orthogroups and other relevant information
_Tables_:
* sequenceTab:
Table including sequences for each gene for easier lookup
  * **id:** gene id as given in sequence file headers in dipteraTranslations_processed/
  * **seq:** associated sequence
* groups_*:
Orthogroup data for different homology inference tools
  * **groupID:** the orthogroup id
  * **groupMembers:** the genes belonging to the orthogroup
* singTrees\_*:
Initial dataset with starting set of _D.suzukii_ singletons including information from data filtering
  * **id:** gene id as given in sequence file headers in dipteraTranslations_processed/
  * **orthogroup:** orthogroup from the tool given in the table name
  * **realGroup:** new group generated from orthologs if needed
  * **baseTree:** Newick string for entire species set as output from IQ-TREE
  * **prunedTree:** Newick string for tree pruned to only species of interest
  * **excludedReason:** Reasons for exclusion of gene from further consideration: NULL if included in next analysis step
  * **split:** For cases where paralogs are detected in the singleton outgroup species, T if the tree can be split (ancestral duplication), F if not (duplication occurred within timeframe of interest)
  * **notes:** Notes whether there are multiple copies detected in the singleton outgroups
  * **tree\_top\_id:** Unique id relating to tree topology as assigned by ete3, reduces the number of manual checks regarding checking for suitability to be split
* procTrees\_*:
Final dataset for analysis, includes filtered singleton set with trees and various attributes
  * **id:** gene id as given in sequence file headers in dipteraTranslations_processed/
  * **tree:** newick string for the final gene tree for each gene
  * **excludedReason:** reason for exclusion from final comparison, NULL if included in final comparison
  * **dup\_status:** classification of the gene as singleton (S) or duplicable (D)
  * **dupInSp:** comma-separated list of species where there are multiple paralogs
  * **confirm\_[rate/dS/dN]:** confirmatory (in group) rates, measured between _D. eugracilis_ and _D. melanogaster_
  * **proxy\_[rate/dS/dN]:** proxy ancestral rates, measured between _D. eugracilis_ and _D. suzukii_
  * **cdsLen:** length of the longest CDS associated with the gene
  * **gc:** % GC content for the longest CDS associated with the gene
  * **gc3:** % GC content at the third codon position for the longest CDS associated with the gene
  * **exp:** expression level given in TPM, quantified using RSEM
  * **possMissedDup:** T if paralogs possibly missed in homology inference are found
  * **possMissedPara:** List of potentially missed paralogs if possMissedDup is T



===========================================================================================================================
## Sequence data

**dipteraCDS_raw/:** .fasta files containing CDS sequences for each species, as downloaded

**dipteraTranslations_raw/:** .fasta files containing translated CDS sequences for each species, as downloaded

**dipteraTranslations_processed/:** .fasta files containing translated CDS sequences for each species, longest sequence for each gene only. Headers are formatted: gene|protein|species


=========================================================================================================
## Figures
**Figures/:** .png versions of figures included in (REF)

=========================================================================================================
## Possible impact of missed paralogs
**Fast\_evolving\_singletons/**: Output files relating to analysis of the impact of faster rate of evolution on duplicate detection
* **dmelBuscoRBH\_insect.txt:** _D. melanogaster_ genes found to the the reciprocal best hit for a set of BUSCO genes as defined in insects - used to determine species distance for abSENSE analysis
* **fes\*.txt:** Files listing genes defined as fast-evolving singletons (95th percentile by rate of singletons) using each homology inference tool
* **restrictionLevels_singTrees_Orthofinder.txt:** Taxonomic restriction levels for fast-evolving singletons defined using Orthofinder

=========================================================================================================
