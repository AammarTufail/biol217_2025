# Metaviromics tutorial

## Viromics reference
* Reference paper for pipeline used: https://journals.asm.org/doi/10.1128/msystems.00888-24 
* Reference GitHub for pipeline used: https://gitlab.com/ccoclet/mvp 

## The pipeline's main steps are:
* The MVP pipeline takes (meta)-genomic assemblies, reads, and metadata as inputs, and performs the following steps:


**! We are not taking credit for the tools, we are simply explaining how they work for an in-house tutorial !** 

## Tools which the MVP pipeline is using as dependencies

|Pipeline modules | Used software/dependencies | Tool version | Github link |
| --- | --- | --- | --- |
| Viruses, proviruses, and plasmid identification | geNomad | 1.7.4 | https://github.com/apcamargo/genomad  |
| Viral Taxonomy | geNomad | 1.7.4 | https://github.com/apcamargo/genomad |
| Quality assessment and filtering | CheckV | 1.0.3 | https://bitbucket.org/berkeleylab/checkv/src/master/ |
| ANI clustering | CheckV | 1.0.3 | https://bitbucket.org/berkeleylab/checkv/src/master/ |
| Abundance estimation | Bowtie2 | 2.5.4 | https://bowtie-bio.sourceforge.net/bowtie2/index.shtml |
| --- | Minimap2 | 2.28 | https://github.com/lh3/minimap2 |
| --- | Samtools | 1.21 | https://www.htslib.org/ |
| --- | CoverM | 0.7.0 | https://github.com/wwood/CoverM |
| Gene function annotation | Prodigal | 2.6.3 | https://github.com/hyattpd/Prodigal  |
| --- | MMseqs2 | 14.7e284 | https://github.com/soedinglab/MMseqs2  |
| --- | HMMER | 3.4 | https://github.com/EddyRivasLab/hmmer |
| --- | DIAMOND | 2.1.0 | https://github.com/bbuchfink/diamond  |
| Viral Binning | vRhyme | 1.1.0 | https://github.com/AnantharamanLab/vRhyme |
| NCBI MIUViG preparation for submission | --- | --- | --- |
| Results visualization | R | --- | --- |
| Prepares data for Viral-host prediction | External: iPhoP | 1.3.3 | https://bitbucket.org/srouxjgi/iphop/src/main/  |



- ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) `We will not run the commands as they take a long time and databases are very large`
