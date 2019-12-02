# RADAR
**RADAR** is devised to detect and visualize all possible twelve-types of RNA editing events from RNA-seq datasets.

## Features
* RADAR (**R**NA-editing **A**nalysis-pipeline to **D**ecode **A**ll twelve-types of **R**NA-editing events) can be conveniently applied to identify RNA-editing from RNA-seq data with stringent filtering steps.
*  Plot tools are also provided to present RNA-editing called from RADAR.

## Installation
RADAR can be run directly without setup process after downloaded and unzipped, only if tools it depends on have been installed:

1. [HISAT2 (v2.1.0)](https://ccb.jhu.edu/software/hisat2/index.shtml)
2. [BWA (v0.7.9)](http://bio-bwa.sourceforge.net/)
3. [Samtools (v1.9)](http://www.htslib.org/)
4. [GATK (v4.1.2.0)](https://software.broadinstitute.org/gatk/)
5. [R (v3.5.1)](https://www.r-project.org)<br/>
    Dependent R packages:
    * [ggplot2](https://ggplot2.tidyverse.org/index.html)
    * [dplyr](https://dplyr.tidyverse.org/index.html)

## Setup
RADAR requires the reference genome and annotations listed as follows:
1. Ribosomal DNA (rDNA) referenece and BWA MEM index
2. reference genome, HISAT2 index, BWA MEM index
3. SNP annotation: dbSNP, 1000Genome, EVS
    * [NCBI dbSNP](http://www.ncbi.nlm.nih.gov/SNP/)
    * [The 1000 Genomes Project](https://www.internationalgenome.org/)
    * [The University of Washington Exome Sequencing Project](http://evs.gs.washington.edu/EVS/)
4. Alu, repetitive non-Alu, non-repetitive annotataion
5. RNA stranded annotation
6. Blat index
7. 4bp

## Pipeline
<img src="https://github.com/xiongyichun/RADAR/blob/master/RADAR.jpg"  alt="RADAR pipeline" />
RADAR pipeline can break down into three main steps:

### STEP 1: RNA-seq read mapping

* paired end:
```
 
 
#!/usr/bin/bash
bash GATK_RNA_seq_HISAT2_BWA_19_9_25.sh RNA_Editing_Calling_Pipeline_HISAT2_BWA_followed_by_GATK_HaplotypeCaller -1 ${path_of_fastq1} -2 ${path_of_fastq2}  -o ${output_dir} -n ${name} -g ${ref_genome} -t ${maximum_threads}
```
* single end:
```bash
#!/usr/bin/bash
bash GATK_RNA_seq_HISAT2_BWA_19_9_25.sh RNA_Editing_Calling_Pipeline_HISAT2_BWA_followed_by_GATK_HaplotypeCaller -s ${path_of_fastq} -o ${output_dir} -n ${name} -g ${ref_genome} -t ${maximum_threads}
```

### STEP 2: RNA editing calling

### STEP 3: RNA editing visualizing

