# What causes antibiotic resistance?

SCAMT bioinformatics course 2022-2023

Plan of the project
1. Preparation
2. Reads quality control
3. Adapters trimming 

## Preparation

1. Create a new directory
<code>mkdir HW1</code>

2. Go to the new directory
<code>cd ./HW1</code>

3. Create a new folder for raw materials and outputs
<code>mkdir ./raw </code>
<code>mkdir ./output </code>

4. Upload the reference genome and its annotation
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz</code>
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz</code>

5. Unzip the downloaded files
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz</code>
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz</code>

6. Upload the reads (amp_res_1.fastq and amp_res_2.fastq) to the ./raw folder manually

## Reads quality control

1. Install FastQC using conda
<code>conda install -c bioconda fastqc</code>

2. 


