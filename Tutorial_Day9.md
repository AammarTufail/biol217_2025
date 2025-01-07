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



🔴 **We will not run the commands as they take a long time and databases are very large**

## Questions

* **How many proviruses in the BGR_140717/ sample
* **How many viruses are in the BGR_140717 sample

- Hint look into folder 01_GENOMAD and find the *.fna virus files. Use grep “?”


<details><summary><b>Finished commands</b></summary>
  
```ssh
grep ">" -c 01_GENOMAD/BGR_140717/BGR_140717_Proviruses_Genomad_Output/proviruses_summary/proviruses_virus.fna

grep ">" -c 01_GENOMAD/BGR_140717/BGR_140717_Viruses_Genomad_Output/BGR_140717_modified_summary/BGR_140717_modified_virus.fna
```
</details>

## Questions

* **How many Caudoviricetes viruses in the BGR_***/ sample? Any other viral taxonomies?

- Briefly look up and describe these viruses (ds/ss DNA/RNA and hosts (euk/prok)

* **How many High-quality and complete viruses in the BGR_***/ sample

- Hint look into folder 02_CHECKV and find the MVP_02_BGR_***_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.ts files. Use grep “?” -?

<details><summary><b>Finished commands</b></summary>
  
```ssh
grep -c "Caudoviricetes" 02_CHECK_V/BGR_***/MVP_02_BGR_***/_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.tsv
```
</details>


* **How many Low-Quality/Medium-quality/High-quality/Complete
  
<details><summary><b>Finished commands</b></summary>
  
```ssh
grep -c "Low-quality" 02_CHECK_V/BGR_***/MVP_02_BGR_***/_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.tsv
```
</details>


What is the length of the complete virus? How many viral hallmark genes?

Check how abundant is your complete virus in the different samples (RPKM)? Look into folders
04_READ_MAPPING/Subfolders/BGR_*_CoverM.tsv and find your viruses.
Create a table and summarize the RPKM value of the virus in the different samples.

Or look into folder 05_VOTU_TABLES


Now let’s look at annotated genes in 06_FUNCTIONAL_ANNOTATION and find the table: 
MVP_06_All_Sample_Filtered_Conservative_Merged_Genomad_CheckV_Representative_Virus_Proviruses_Gene_Annotation_GENOMAD_PHROGS_PFAM_Filtered.tsv



Now find/filter your complete virus and find the viral hallmark genes with a PHROG annotation (hint: look at the columns).
What are typical annotations you see? What could the functions be?  


Now look for the category of “moron, auxiliary metabolic gene and host takeover” any toxin genes???? Quickly look up the function of this toxin (hint, vibrio phage and vibrio cholerae host)

Now let’s look at the binning results
Look at 07_BINNING/07C_vBINS_READ_MAPPING/  and find table MVP_07_Merged_vRhyme_Outputs_Unfiltered_best_vBins_Memberships_geNomad_CheckV_Summary_read_mapping_information_RPKM_Table.tsv


How many High-quality viruses after binning in comparison to before binning? (hint: look carefully at the table, it has duplicate entries for bins)

Are any of the identified viral contigs complete circular genomes (based on identifying direct terminal repeat regions on both ends of the genome)?


You can also look at the table  07D_vBINS_vOTUS_TABLES and find table: MVP_07_Merged_vRhyme_Outputs_Filtered_conservative_best_vBins_Representative_Unbinned_vOTUs_geNomad_CheckV_Summary_read_mapping_information_RPKM_Table.tsv


Now finally let’s have a look at the potential predicted host of these complete viruses.
Look into folder 08_iPHoP 




