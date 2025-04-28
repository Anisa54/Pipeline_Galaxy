# Pipeline_Galaxy

Step 1:
Upload: RMH200SolidBRCA_Blend-T_S185_R1_001.fastq and RMH200SolidBRCA_Blend-T_S185_R2_001.fastq

Step 2: Run FASTQ QC metric
input: RMH200SolidBRCA_Blend-T_S185_R1_001.fastq on the FASTQ Read Quality report tool
Error occured: FASTQC is expecting a valid .gz file, but its trying to unzip it and hitting data that doesnt look like a GZIP-compressed content
Output: application/gzip 
        Picked up _JAVA_OPTIONS: -Djava.io.tmpdir=/jetstream2/scratch/main/jobs/67049117/tmp -Xmx47002m -Xms256m
        Failed to process HaemoncPromega_Pos-T_S184_R1_001_fastq.gz
        java.util.zip.ZipException: Not in GZIP format at java.base/java.util.z
Error Fixed: Renamed the datatype, fastqs.gz TO fastersanger
saved new and ran FASTQC again

Step 3: Allignment to refrence genome (hg19), created BAM file using BWA-MEM tool
Input: your fastersanger files (s)
Ouput: BAM file created 

Step 4: Sort and

Type:Samtool sort
click "sort BAM dataset"
set the following: "BAM dataset to sort" --> your BAM file (output for allignment)
click execute 
    #sorted BAM = reads are on order by genomic cordinates

Step 5:Post Allignment full QC 

A) Input: Use tool Mark Duplicate, BAM sorted file used

B) Qualimap BAM QC
Input: your duplicate-marked BAM file
Refrence Genome = same one used during allignment




