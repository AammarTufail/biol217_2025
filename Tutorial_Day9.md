# Metaviromics tutorial

## Viromics reference

* Reference paper for MVP pipeline used: https://journals.asm.org/doi/10.1128/msystems.00888-24 
* Reference GitHub for pipeline used: https://gitlab.com/ccoclet/mvp 
* Reference paper for iPHoP pipeline used: [https://journals.asm.org/doi/10.1128/msystems.00888-24](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.3002083)
  
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


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
🔴 **Here are the exact command lines used**

# MVP
```
module load gcc12-env/12.1.0
module load micromamba/1.3.1
micromamba activate MVP
cd $WORK/MVP_test
mvip MVP_00_set_up_MVP -i ./WORKING_DIRECTORY/ -m input_file_timeseries_final.csv  --genomad_db_path ./WORKING_DIRECTORY/00_DATABASES/genomad_db/ --checkv_db_path ./WORKING_DIRECTORY/00_DATABASES/checkv-db-v1.5/
mvip MVP_00_set_up_MVP -i ./WORKING_DIRECTORY/ -m input_file_timeseries_final.csv  --skip_install_databases
mvip MVP_01_run_genomad_checkv -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_02_filter_genomad_checkv -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_03_do_clustering -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_04_do_read_mapping -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv --delete_files
mvip MVP_05_create_vOTU_table -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_06_do_functional_annotation -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
mvip MVP_07_do_binning -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv --force_outputs
mvip MVP_100_summarize_outputs -i WORKING_DIRECTORY/ -m input_file_timeseries_final.csv
```

# iPHoP
```
module load miniconda3/4.12.0
conda activate GTDBTk
export GTDBTK_DATA_PATH=./GTDB_db/GTDB_db

gtdbtk de_novo_wf --genome_dir fa_all/ \
--bacteria --outgroup_taxon p__Patescibacteria \
--out_dir output/ \
--cpus 12 --force --extension fa

gtdbtk de_novo_wf --genome_dir fa_all/ \
--archaea --outgroup_taxon p__Altarchaeota \
--out_dir output/ \
--cpus 12 --force --extension fa

module load micromamba/1.3.1
micromamba activate iphop_env
iphop add_to_db --fna_dir fa_all/ \
--gtdb_dir ./output/ \
--out_dir ./MAGs_iPHoP_db \
--db_dir iPHoP_db/

iphop predict --fa_file ./MVP_07_Filtered_conservative_Prokaryote_Host_Only_best_vBins_Representative_Unbinned_vOTUs_Sequences_iPHoP_Input.fasta \
--db_dir ./MAGs_iPHoP_db \
--out_dir ./iphop_output -t 12
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

- Hint look into folder 02_CHECKV and find the `MVP_02_BGR_***_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.tsv` files. Use grep “?” -?

<details><summary><b>Finished commands</b></summary>
  
```ssh
grep -c "Caudoviricetes" 02_CHECK_V/BGR_***/MVP_02_BGR_***/_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.tsv
```
</details>

## Questions

* **How many Low-Quality/Medium-quality/High-quality/Complete
  
<details><summary><b>Finished commands</b></summary>
  
```ssh
grep -c "Low-quality" 02_CHECK_V/BGR_***/MVP_02_BGR_***/_Filtered_Relaxed_Merged_Genomad_CheckV_Virus_Proviruses_Quality_Summary.tsv
```
</details>

## Questions

* **What is the length of the complete virus? How many viral hallmark genes?
* **Check how abundant is your complete virus in the different samples (RPKM)? Look into folders `04_READ_MAPPING/Subfolders/BGR_*_CoverM.tsv` and find your viruses.
* **Create a table and summarize the RPKM value of the virus in the different samples. Or look into folder 05_VOTU_TABLES

## Questions
* Now let’s look at annotated genes in 06_FUNCTIONAL_ANNOTATION and find the table: 
`MVP_06_All_Sample_Filtered_Conservative_Merged_Genomad_CheckV_Representative_Virus_Proviruses_Gene_Annotation_GENOMAD_PHROGS_PFAM_Filtered.tsv`

* Now find/filter your complete virus and find the viral hallmark genes with a PHROG annotation (hint: look at the columns).

* **What are typical annotations you see? What could the functions be?  

* **Now look for the category of “moron, auxiliary metabolic gene and host takeover” any toxin genes???? Quickly look up the function of this toxin (hint, vibrio phage and vibrio cholerae host)

*Now let’s look at the binning results. Look at 07_BINNING/07C_vBINS_READ_MAPPING/ and find table `MVP_07_Merged_vRhyme_Outputs_Unfiltered_best_vBins_Memberships_geNomad_CheckV_Summary_read_mapping_information_RPKM_Table.tsv`


## Questions

* **How many High-quality viruses after binning in comparison to before binning? (hint: look carefully at the table, it has duplicate entries for bins)
* **Are any of the identified viral contigs complete circular genomes (based on identifying direct terminal repeat regions on both ends of the genome)?


*You can also look at the table  07D_vBINS_vOTUS_TABLES and find table: `MVP_07_Merged_vRhyme_Outputs_Filtered_conservative_best_vBins_Representative_Unbinned_vOTUs_geNomad_CheckV_Summary_read_mapping_information_RPKM_Table.tsv`


*Now finally let’s have a look at the potential predicted host of these complete viruses.
*Look into folder 08_iPHoP and find table: `Host_prediction_to_genome_m90.csv`
* **What are the predicted hosts for your complete virus? are there multiple predicted hosts? are the hosts distantly related? 
* if not find 2 examples of viruses with multiple hosts predicted. for virus 1 closely related hosts and for virus 2 distantly related hosts. 
* Discuss what might be the reasons based on 1) biological reasoning, 2) the prediction method or 3) potential contamination in host MAG that migh result in such a prediction.



