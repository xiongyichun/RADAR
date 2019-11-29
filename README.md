# RADAR
**RADAR** is devised to detect and visualize all possible twelve-types of RNA editing events from RNA-seq datasets.

## Features
* RADAR (**R**NA-editing **A**nalysis-pipeline to **D**ecode **A**ll twelve-types of **R**NA-editing events) can be conveniently applied to identify RNA-editing from RNA-seq data with stringent filtering steps.
*  Plot function is also provided to present RNA-editing called from RADAR.

## Installation
RADAR itself does not require installation, just download and unzip. But it depends on several tools required to be installed:

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
3. SNP: dbSNP, 1000Genome, EVS
    * [NCBI dbSNP](http://www.ncbi.nlm.nih.gov/SNP/)
    * [The 1000 Genomes Project](https://www.internationalgenome.org/)
    * [The University of Washington Exome Sequencing Project](http://evs.gs.washington.edu/EVS/)
    SNP annotation file
4. Alu, repetitive non-Alu, non-repetitive annotataion

