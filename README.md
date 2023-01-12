# What causes antibiotic resistance?

SCAMT bioinformatics course 2022-2023

Plan of the project
1. Get data
2. Get to know data
3. 


## Get data

Create a new directory <p>
<code>mkdir HW1</code>

Go to the new directory <p>
<code>cd ./HW1</code>

Create new folders for raw materials and outputs <p>
<code>mkdir ./raw </code> <p>
<code>mkdir ./output </code>

Upload the reference genome and its annotation <p>
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz </code> <p>
<code>wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz </code>

Unzip the downloaded files<p>
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz</code> <p>
<code>gunzip GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz</code>

Upload the reads (amp_res_1.fastq and amp_res_2.fastq) to the ./raw folder manually <p>

## Get to know data

<code>head -20 amp_res_1.fastq</code><p>
<code>head -20 amp_res_2.fastq</code><p>
<code>cat GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna</code><p>
<code>cat GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff</code><p>

## Control reads quality

Install FastQC using conda <p>
<code>conda install -c bioconda fastqc</code>

Quality control <p>
<code>fastqc ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq -o ./output </code>

## Trim
  
Install Trimmomatic<p>
<code>conda create -n trimmomatic -c bioconda -c conda-forge -c defaults trimmomatic</code>

Deactivate conda<p>
<code>conda deactivate</code>

Activate Trimmomatic<p>
<code>conda activate trimmomatic</code>

Trimming with defined parameters<p>
<code>trimmomatic PE -phred33 ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq paired1.fq single1.fq paired2.fq single2.fq LEADING:20 TRAILING:20 SLIDINGWINDOW:10:20 MINLEN:20 ILLUMINACLIP:/home/donya/anaconda3/pkgs/trimmomatic-0.39-hdfd78af_2/share/trimmomatic-0.39-2/adapters/TruSeq3-PE-2.fa:2:30:10</code><p>
<code>LEADING:20</code> - <p> 
<code>TRAILING:20</code> - <p>
<code>SLIDINGWINDOW:10:20</code> - <p> 
<code>MINLEN:20</code>- <p>  

<code>trimmomatic PE -phred33 ./raw/amp_res_1.fastq ./raw/amp_res_2.fastq 30_paired1.fq 30_single1.fq 30_paired2.fq 30_single2.fq LEADING:30 TRAILING:30 SLIDINGWINDOW:10:30 MINLEN:20 ILLUMINACLIP:/home/donya/anaconda3/pkgs/trimmomatic-0.39-hdfd78af_2/share/trimmomatic-0.39-2/adapters/TruSeq3-PE-2.fa:2:30:10</code><p>

<code>LEADING:30</code> - <p>  
<code>TRAILING:30</code> - <p> 
<code>SLIDINGWINDOW:10:30</code> - <p> 
<code>MINLEN:20</code> - <p>
  
Activate conda<p>
<code>conda activate</code>

Quality control<p>
<code>fastqc paired1.fq paired2.fq -o ./output</code><p>
<code>fastqc 30_paired1.fq 30_paired2.fq -o ./output</code> 
  
## Align
  
Install BWA<p>
<code>conda install -c bioconda bwa</code><p>

 <p>
<code>bwa index ./raw/GCF_000005845.2_ASM584v2_genomic.fna</code><p>

 <p>
<code>bwa mem ./raw/GCF_000005845.2_ASM584v2_genomic.fna paired1.fq paired2.fq > alignment.sam</code><p>

## Compress SAM file to BAM

<p>
<code> conda install -c bioconda samtools</code><p>

<p>
<code>samtools view -S -b alignment.sam > alignment.bam</code><p>

<p>
<code>samtools flagstat alignment.bam</code><p>

## Sort and index BAM file 

 <p>
<code>samtools sort alignment.bam -o alignment_sorted.bam</code><p>

<p>
<code>samtools index alignment_sorted.bam</code><p>

Go to IGV browser (https://igv.org/app/)<p>
Genome -> Local file (.fasta + .fasta.fai)<p>
Tracks -> Local file (.bam + .bam.bai)<p>

## Call variants

<p>
<code>samtools mpileup -f ./raw/GCF_000005845.2_ASM584v2_genomic.fna alignment_sorted.bam > my.mpileup</code><p>

<p>
<code>conda install -c bioconda varscan</code>

<p>
<code>varscan mpileup2snp my.mpileup —min-var-freq 0.70 —variants —output-vcf 1 > VarScan_results.vcf</code>

## Predict variant effect
Go to IGV browser (https://igv.org/app/)<p>
Genome -> Local file (.fasta + .fasta.fai)<p>
Tracks -> Local file (.gff)<p>
Tracks -> Local file (.bam + .bam.bai)<p>
Tracks -> Local file (.vcf)<p>

<p>
<code>cat VarScan_results.vcf</code>


  
