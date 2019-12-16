# RADAR
**RADAR** is devised to detect and visualize all possible twelve-types of RNA editing events from RNA-seq datasets.
## Features
RADAR (**R**NA-editing **A**nalysis-pipeline to **D**ecode **A**ll twelve-types of **R**NA-editing events) can be conveniently applied to identify RNA-editing from RNA-seq data with stringent filtering steps.
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
```

## Configuration
Reference genome, genomic sequence index for aligners and genomic annotations should be provided to RADAR in the Config.txt file:
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

## Pipeline

RADAR pipeline can break down into three main steps:

### STEP 1: RNA-seq read mapping

* paired end:

```bash
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
1. Summarize all 12 types of RNA-editing into an Excel file
2. Histogram plot for each treatment
3. Manhattan plot of specific RNA-editing type 
