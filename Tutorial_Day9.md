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
| Viruses, proviruses, and plasmid identification | geNomad | 1.7.4 | [geNomad link](https://github.com/apcamargo/genomad ) |
| Viral Taxonomy | --- | --- | --- |
| Quality assessment and filtering | --- | --- | --- |
| ANI clustering | --- | --- | --- |
| Abundance estimation | --- | --- | --- |
| Gene function annotation | --- | --- | --- |
| Viral Binning | vRhyme | 1.1.0 | https://github.com/AnantharamanLab/vRhyme |
| NCBI MIUViG preparation for submission | --- | --- | --- |
| Results visualization | R | --- | --- |
| Prepares data for Viral-host prediction | External: iPhoP | 1.3.3 | https://bitbucket.org/srouxjgi/iphop/src/main/  |
