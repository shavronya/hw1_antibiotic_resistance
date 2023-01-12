# What causes antibiotic resistance?

SCAMT bioinformatics course 2022-2023

Plan of the project
1. Preparation
2. Reads quality control
3. Adapters trimming 

## Preparation 

1. Create a new directory <p>
<code>mkdir HW1</code>

2. Go to the new directory <p>
<code>cd ./HW1</code>

3. Create a new folder for raw materials and outputs <p>
<code>mkdir ./raw </code> <p>
<code>mkdir ./output </code>

4. Upload the reference genome and its annotation <p>
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz </code> <p>
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz </code>

5. Unzip the downloaded files <p>
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz</code> <p>
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz</code>

6. Upload the reads (amp_res_1.fastq and amp_res_2.fastq) to the ./raw folder manually <p>

## Reads quality control

1. Install FastQC using conda <p>
<code>conda install -c bioconda fastqc</code>

2. Quality control <p>
<code>fastqc ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq -o ./output </code>

## Trimming
  
1. Install Trimmomatic<p>
<code>conda create -n trimmomatic -c bioconda -c conda-forge -c defaults trimmomatic</code>

2. Deactivate conda<p>
<code>conda deactivate</code>

3. Activate Trimmomatic<p>
<code>conda activate trimmomatic</code>

4. Trimming with defined parameters<p>
<code>trimmomatic PE -phred33 ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq paired1.fq single1.fq paired2.fq single2.fq LEADING:20 TRAILING:20 SLIDINGWINDOW:10:20 MINLEN:20 ILLUMINACLIP:/home/donya/anaconda3/pkgs/trimmomatic-0.39-hdfd78af_2/share/trimmomatic-0.39-2/adapters/TruSeq3-PE-2.fa:2:30:10</code><p>
<code>LEADING:20</code><p> - 
<code>TRAILING:20</code><p> - 
<code>SLIDINGWINDOW:10:20 </code><p> - 
<code>MINLEN:20</code><p> - 


<code>trimmomatic PE -phred33 ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq 30_paired1.fq 30_single1.fq 30_paired2.fq 30_single2.fq LEADING:30 TRAILING:30 SLIDINGWINDOW:10:30 MINLEN:20 ILLUMINACLIP:/home/donya/anaconda3/pkgs/trimmomatic-0.39-hdfd78af_2/share/trimmomatic-0.39-2/adapters/TruSeq3-PE-2.fa:2:30:10</code><p>

<code>LEADING:30</code><p> - 
<code>TRAILING:30</code><p> - 
<code>SLIDINGWINDOW:10:30 </code><p> - 
<code>MINLEN:20</code><p>
  
5. Activate conda<p>
<code>conda activate</code>

6. Quality control <p>
<code>fastqc paired1.fq paired2.fq -o ./output</code>
<code>fastqc 30_paired1.fq 30_paired2.fq -o ./output</code>
  
7. 
