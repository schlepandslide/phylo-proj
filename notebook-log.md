added datasets from: https://pmc.ncbi.nlm.nih.gov/articles/PMC8389581/#_ad93_
four distinct sheets, will need to combine or pick one set

#2/20/25
- removed old data set, new data comes from ncbi. see the fna file for more info
- Used MUSCLE on new data: pseudomonas.fna
- should be aligned?

#3/4/25
- updated fasta alignments
- wrote r script using ape and pranghorn
	- follows the same process as class, except uses njs() due to an error

#3/20/25
- replaced the dataset once again, say hello to the rpsP gene of *Pseudomonas*
- chose IQ-Tree as my software for max. likelihood
	- mainly due to RAxML not running on windows
		-Pros: runs on windows, Fast!, command-line based
		-Cons: Bias prone, relies on simplification
		-Assumptions: Treelikeness, homogeneity

sample code/commands:
	
.\iqtree -s pseudomonas-s16.fasta -bb 1000 -nt AUTO #basic ML reconstruction
.\iqtree -s pseudomonas-s16.fasta -spp pseudomonas-s16.nxs -bb 1000 -nt AUTO #partition model finder
.\iqtree -s pseudomonas-s16.fasta -spp pseudomonas-s16.nxs -bb 1000 -nt AUTO -m MFP+MERGE -rcluster 10 -pre pseudomonas-s16.merge #partition model merge
.\type pseudomonas-s16.fasta.treefile pseudomonas-s16.nxs.treefile >pseudomonas-s16.trees #log-likelihood test
.\iqtree -s pseudomonas-s16.fasta -spp pseudomonas-s16.nxs.best_scheme.nxs -z pseudomonas-s16.trees -zb 1000 -n 0 -wpl -pre pseudomonas-s16.test #pass on

TBD: iq-tree beta code?

.\iqtree -s pseudomonas-s16.fasta -spp pseudomonas-s16.nxs -bb 1000 -nt AUTO -bsam GENESITE -pre pseudomonas-s16.bsam
