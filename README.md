# Pipeline_Galaxy

**Step 1:**
Upload: RMH200SolidBRCA_Blend-T_S185_R1_001.fastq and RMH200SolidBRCA_Blend-T_S185_R2_001.fastq

**step 2**  Run FASTQ QC metric
input: RMH200SolidBRCA_Blend-T_S185_R1_001.fastq on the FASTQ Read Quality report tool
Error occured: FASTQC is expecting a valid .gz file, but its trying to unzip it and hitting data that doesnt look like a GZIP-compressed content
Output: application/gzip 
        Picked up _JAVA_OPTIONS: -Djava.io.tmpdir=/jetstream2/scratch/main/jobs/67049117/tmp -Xmx47002m -Xms256m
        Failed to process HaemoncPromega_Pos-T_S184_R1_001_fastq.gz
        java.util.zip.ZipException: Not in GZIP format at java.base/java.util.z
Error Fixed: Renamed the datatype, fastqs.gz TO fastersanger
saved new and ran FASTQC again

**Step 3:** Allignment to refrence genome (hg19), created BAM file using BWA-MEM tool
Input: your fastersanger files (s)
Ouput: BAM file created 
        #BWA-MEM used to align R1 and R2 to a reference genome, output in BAM format

**Step 4:** Sort 

Type:Samtool sort
click "sort BAM dataset"
set the following: "BAM dataset to sort" --> your BAM file (output for allignment)
click execute 
    #sorted BAM = reads are on order by genomic cordinates

**Step 5**:Post Allignment QC 

Type:Samtools idxstats
Input: Sorted BAM file
Output: Tabular format 

Type:Samtools flagstat
Input:Sorted BAM file
Output: metrics.txt format with QC values 

Type: Picard MarkDuplicates
Input: BAM from BWA-MEM 
        # parameters used:
        Remove duplicates? No → This is what you want. It will mark duplicates (flag them), not delete them.
        Assume sorted? Yes → Good. Your BAM has already been sorted (step 8).
        Scoring strategy: SUM_OF_BASE_QUALITIES → Default and recommended. It keeps the best-quality read as the non-duplicate.
Output: Deduplicated BAM where duplicates are marked (flagged, not removed)

**Step 6: MultiQC** - It aggregates results from many bioinformatics tools (like FastQC, Samtools, Picard, etc.) into a single report. This helps spot trends, issues, or anomalies across sample

Intervals file: BRCADirect.v1.0.bed.intervals
