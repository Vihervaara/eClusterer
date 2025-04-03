
# General info and input files

This code takes in coordinates of transcribed enhancers and finds clusters of enhancers (eCLusters).
The coordinates of enhancers (chromosome, start, end) are been obtained from Precision Run-On Sequencing (PRO-seq) data as divergent transcription distal to annotated genes TSSs.

The eCLusterer has been developed and verified with dog macrophage cells (Himanen et al., 2025 bioRxiv), and can be used across species (unpublished).
The code recognised known super-enhancers, such as MYC super-enhancer (active in various cancers), and EMB super-enhancer (shown to be active in macrophages).




# CITATION OF eCLUSTERER:
To cite the eClusterer and see verification of MYC and EMB super-enhancer in dog:

Himanen SV, Rabenius A, Aktay S, Tekoniemi J, Vihervaara A (2025). 
Transcriptional architecture and Pol II regulation at promoters, enhancers, and enhancer clusters in Canis lupus familiaris. 
https://www.biorxiv.org/content/10.1101/2025.03.20.644285v1



# Additional References 
To dentify transcribed enhancers from PRO-seq data:
https://doi.org/10.1016/j.xpro.2021.101036
http://www.genome.org/cgi/doi/10.1101/gr.238279.118.

Known super-enhancers have been obtained from an atlas of super-enhancers: 
https://academic.oup.com/nar/article/44/D1/D164/2502575. 








# INFO for running: 

This code uses shell and R.

## Naming enhancer coordinates:
 The code requires enhancer coordinates to be given either:
 i) in columns named: chr, eStart, eEnd
 ii) reside in columns 1:3

The code starts by checking, whether the expected names (chr, eStart, eEnd) are present in the input file.
If yes, the code continues. If not, columns 1:3 are named "chr", "eStart", "eEnd" , whereafter the code continues.


## FIRST PART, in R: Seeding clusters
 Generates preliminary clusters based on parameters:
 i)    Seed window. [Default: 12500 nt].
 ii)   Number of enhancers required in the seed window. [Default: 5 enhancers]
 iii)  Extension window to search additional, adjacent enhancers. [Default: 2000 nt]


## SECOND PART, in shell:  Merging prelimiary coordinates into eClusters
 The initial clusters are combined if they overlap or touch (head-to-tail) using bedtool merge. Output => eClusters.
 The eClusters are intersected with enhancers to match each eCluster with its consituting enhancers. 
     =>    These files can be used as eClusters and their enhancers. 

## OPTIONAL THIRD PART, in R:  expression filter and visualization files
 Adds a threshold (default eRNA > 5) for enhancers that consitute eClusters.
 Analyses transcriptional change (in the original code, heat-induced change) in eClusters. It requires the file to have eRNA values from the control and treatment conditions.
 Genrates output files that can be openend in a genome browser to visualize eCLuster coordinates.


