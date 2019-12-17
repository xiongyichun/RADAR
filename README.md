# RADAR
**RADAR** (**R**NA-editing **A**nalysis-pipeline to **D**ecode **A**ll twelve-types of **R**NA-editing events) is devised to detect and visualize all possible twelve-types of RNA editing events from RNA-seq datasets.
## Features
RADAR can be conveniently applied to identify RNA-editing from RNA-seq data with stringent filtering steps.
* All possible RNA-editing events from each given RNA-seq dataset are summarized into an Excel file.
* Numbers of all twelve-types of RNA editing events are plotted by histograms according to their genomic locations in Alu, repetitive non-Alu and non-repetitive regions.
* Manhattan plots are further used to illustrate RNA editing ratios of selected types of RNA-editing events, such as C-to-U or A-to-G.

## Schema
<img src="https://github.com/xiongyichun/RADAR/blob/master/docs/RADAR.jpg"  alt="RADAR pipeline" />

## Installation requirements
RADAR can be run directly without setup process after downloaded and unzipped, only if tools it depends on have been installed:

1. [HISAT2 (>=2.0.5)](https://ccb.jhu.edu/software/hisat2/index.shtml)
2. [BWA (>=0.7.9)](http://bio-bwa.sourceforge.net/)
3. [Samtools (>=1.7)](http://www.htslib.org/)
4. [GATK (>=4.0.1.0)](https://software.broadinstitute.org/gatk/)
5. [R (>=3.0.2)](https://www.r-project.org)<br/>
    Dependent R packages:
    * [ggplot2](https://ggplot2.tidyverse.org/index.html)
    * [dplyr](https://dplyr.tidyverse.org/index.html)
    
## Installation
As long as all **Installation requirements** have been fulfilled, RADAR can be run directly without setup process after downloaded and unzipped. 
```bash
git clone https://github.com/YangLab/RADAR
cd RADAR
chmod +x RADAR
./RADAR
```

## Configuration
Reference genome, genomic sequence index and genomic annotations should be provided to RADAR in the RADAR.conf file:
1. Ribosomal DNA (rDNA) referenece and BWA MEM index
2. reference genome, HISAT2 index, BWA MEM index
3. GATK reference genome index (.dict)
`gatk CreateSequenceDictionary -R hg38_all.fa`
4. Blat index: `tools/ucsc/faToTwoBit hg38_all.fa hg38_all.fa.2bit`
5. SNP annotation: dbSNP, 1000Genome, EVS
    * [NCBI dbSNP](http://www.ncbi.nlm.nih.gov/SNP/) (gatk IndexFeatureFile -F NCBI_dbSNP_b151_all_hg38.vcf )
    * [The 1000 Genomes Project](https://www.internationalgenome.org/)
    * [The University of Washington Exome Sequencing Project](http://evs.gs.washington.edu/EVS/)
6. Alu, repetitive non-Alu, non-repetitive annotataion
7. RNA stranded annotation
8. 4bp
#### Reference and sequence index
1. Ribosomal DNA (rDNA) sequence index for BWA MEM ( Example of command: bwa index \~/reference/Human/RNA_45S5/RNA45S5.fa )<br />
     * Example: `rDNA_idnex_bwa_mem=~/reference/Human/RNA_45S5/RNA45S5.fa`
2. Path to reference genome <br />
     * Example: `genome_fasta=~/reference/Human/hg38/hg38_all.fa`
3. Reference genome sequence index for HISAT2 ( Example of command: hisat2-build \~/reference/Human/hg38/hg38_all.fa \~/reference/Human/hg38/hg38_all.fa ) <br />
 * Example: `genome_index_hisat2=~/reference/Human/hg38/hg38_all.fa`
4. Reference genome sequence index for BWA MEM ( Example of command: bwa index \~/reference/Human/hg38/hg38_all.fa ) <br />
 * Example: `genome_index_bwa_mem=~/reference/Human/hg38/hg38_all.fa`
5. Reference genome sequence index for Blat ( Example of command: tools/faToTwoBit \~/reference/Human/hg38/hg38_all.fa \~/reference/Human/hg38/hg38_all.fa.2bit ) <br />
 * Example: `genome_index_blat=~/reference/Human/hg38/hg38_all.fa.2bit`
6. Reference genome sequence index for GATK in the directory of reference genome ( Example of command: gatk CreateSequenceDictionary -R \~/reference/Human/hg38/hg38_all.fa ) <br />
 * Example: `genome_index_gatk=~/reference/Human/hg38/hg38_all.dict`



#### SNP annotation: dbSNP, 1000Genome, EVS
1. SNP annotation from NCBI dbSNP. Both the total [NCBI dbSNP](http://www.ncbi.nlm.nih.gov/SNP/) .vcf file and folder for NCBI dbSNP divided by chromosome  <br />
 * Example of the total .vcf file: `SNP_dbSNP_all=~/annotation/Human/hg38/SNP/dbSNP_b151/NCBI_dbSNP_b151_all_hg38.vcf`<br />
 * Example of the GATK index for total .vcf (Example of command: gatk IndexFeatureFile -F \~/annotation/Human/hg38/SNP/dbSNP_b151/NCBI_dbSNP_b151_all_hg38.vcf ): `SNP_dbSNP_all_index_gatk=~/annotation/Human/hg38/SNP/dbSNP_b151/NCBI_dbSNP_b151_all_hg38.vcf.idx ` <br />
 * Example of the folder for NCBI dbSNP divided by chromosome: `SNP_dbSNP_divided_by_chromosome=~/annotation/Human/hg38/SNP/dbSNP_b151/split_chr`
2. SNP annotation from [The 1000 Genomes Project](https://www.internationalgenome.org/) divided by chromosome <br />
 * Example of the folder for SNP divided by chromosome: `SNP_1000Genome_divided_by_chromosome=~/annotation/Human/hg38/SNP/1000genomes/split_chr`
3. SNP annotation from [The University of Washington Exome Sequencing Project](http://evs.gs.washington.edu/EVS/) divided by chromosome <br />
 * Example of the folder for SNP divided by chromosome: `SNP_EVS_divided_by_chromosome=~/annotation/Human/hg38/SNP/EVS/split_chr`


#### Genome annotation
1. Annotation of Alu, repetitive non-Alu, non-repetitive genomic region in the BED format <br />
 * Example of Alu annotation: `annotation_Alu=~/annotation/Human/hg38/Alu.bed ` <br />
 * Example of repetitive non-Alu annotation: `annotation_Repetitive_non-Alu=~/annotation/Human/hg38/Repetitive_non-Alu.bed` <br />
 * Example of all repetitive annotation: `annotation_All_repetitive=~/annotation/Human/hg38/All_repetitive.bed` <br />
2. Annotation of RepeatMasker simple repeats from UCSC in BED format <br />
 * Example: `annotation_simple_repeats=~/annotation/Human/hg38/UCSC_RepeatMask_SimpleRepeats_hg38.bed`
3. Annotation of splice sites from UCSC in BED format <br />
 * Example: `annotation_splice_sites=~/annotation/Human/hg38/ref_all_spsites_hg38.bed`
4. Annotation of intronic 4 bp <br />
 * Example: `annotation_intronic_4site=~/annotation/Human/hg38/hg38_intronic_4site.bed`
5. Annotation of transcribed strands of genes <br />
 * Example: `annotation_gene_transcribed_strands=~/annotation/Human/hg38/ref_all_6.bed`




## Pipeline

RADAR pipeline can break down into three main steps:

### STEP 1: RNA-seq read mapping

* paired end:

```bash
#!/usr/bin/bash
./RADAR mapping_and_call_RNA_editing -1 ${path_of_fastq1} -2 ${path_of_fastq2}  -o ${output_dir} -n ${name} -g ${ref_genome} -t ${maximum_threads}
```

* single end:
```bash
#!/usr/bin/bash
./RADAR mapping_and_call_RNA_editing -s ${path_of_fastq} -o ${output_dir} -n ${name} -g ${ref_genome} -t ${maximum_threads}
```

### STEP 2: RNA editing calling

### STEP 3: RNA editing visualizing
1. Summarize all 12 types of RNA-editing into an Excel file
2. Histogram plot for each treatment
3. Manhattan plot of specific RNA-editing type 
