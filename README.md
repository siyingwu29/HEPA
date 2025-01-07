# HEPA
Host expression profiling analysis
## Content
Firstly STAR builds the genome index, then performs the alignment; 
Secondly RSEM builds the index, and then transcript quantification.
## Introduction
STAR (Spliced Transcripts Alignment to a Reference), an alignment software for aligned sequenced Reads to the reference genome, is commonly used in RNA library-based sequencing methods. It owns high accuracy, but needs to occupy a lot of memory, high requirements on computing resources.

The RSEM (RNA-Seq by Expectation-Maximization) is the software for the quantitative estimation of the expression levels of genes and transcripts from the RNA-Seq data. It processes high precision quantification, supports a variety of comparison software as well as outputs more detailed quantitative informations. However,it needs more computing resources and the computing speed is slow.
## Previous preparation
If you run in the terminal, you need to build an environment to install both STAR and RSEM software with conda or mamba.

If you run on the cloud platform, just find it in the workflow, and select the corresponding file to run.The relevant cloud platform address is attached below:https://cloud.stomics.tech/#/project-management/P20Z10200N0206/workflow/workflow/detail?id=66b45aeea015b326032a4404&type=private&jumpType=workflow&version=Version.1.0.0&isPublic=private&fromProjectId=P20Z10200N0206&origin=&hasInToolbox=false

### Use on the terminal
#### Software installation
Create a new environment named transcriptome to install STAR, RSEM
```
conda create -n transcriptome
conda activate transcriptome
```

Install the STAR and the RSEM
```
conda install -c bioconda star
conda install -c bioconda rsem
```

If you want to know if STAR and RSEM have been installed successfully, you could need to use the following command:
```
STAR --help
rsem --help
```
--Help lets you quickly understand the parameters of the software.

#### Software use
##### STAR build index:
```
STAR --runThreadN 6 --runMode genomeGenerate \
             --genomeDir /your/star_index/directory \
             --genomeFastaFiles /your/reference_genome/path \
             --sjdbGTFfile /your/annotation_file/path \
             --sjdbOverhang 149
```

##### Parameter interpretation of the STAR construct index:
–runMode genomeGenerate：Genome generation patterns

–runThreadN：the number of threads

–genomeDir：Index output path

-genomeFastaFiles:Reference genome pathways

–sjdbGTFfile：Reference genome annotation file pathways

–sjdbOverhang：For reads of different lengths, the ideal value is- -sjdbOverhangmax (ReadLength) -1. In most cases, the default value of 100 is similar to the ideal value.




##### STAR alignment:
```
STAR --twopassMode Basic \
             --quantMode TranscriptomeSAM GeneCounts \
             --runThreadN 6 \
             --genomeDir /your/star_index/directory \
             --outSAMtype BAM SortedByCoordinate \
             --sjdbOverhang 149 \
             --outFilterMismatchNmax 2 \
             --outSJfilterReads Unique \
             --outSAMmultNmax 1 \
             --outFileNamePrefix /your/star_results/prefix \
             --outSAMmapqUnique 60 \
             --readFilesCommand gunzip -c \
             --readFilesIn /your/fastq1/path /your/fastq2/path
```
##### Parameter interpretation of the STAR alignment：
–outSAMtype BAM SortedByCoordinate: Output the sorted bam file

–outFileNamePrefix：Prefix of the output file

-readFilesCommand zcat: When using a fastq file compressed by gzip

–readFilesIn：The path of the input fastq files
······
Most are default, and usually you just need to change the contents of a few of these parameters.

You will get a series of STAR results, the important of which are /your/star_results/prefixAligned.sortedByCoord.out.bam and /your/star_results/prefixAligned.toTranscriptome.out.bam. We will use the two files for the next step of transcript alignment.Here I only show the use of the file that is /your/star_results/prefixAligned.toTranscriptome.out.bam.


##### RSEM build index:
```
rsem-prepare-reference --gtf /your/annotation_file/path /your/reference_genome/path /your/rsem_index/prefix -p 8
```


##### RSEM performed the transcriptome alignment:
```
rsem-calculate-expression --paired-end --no-bam-output \
            --alignments -p 8 /your/star_results/prefixAligned.toTranscriptome.out.bam /your/rsem_index/prefix /your/rsem_results/prefix
```

You will get a series of RSEM results, the important of which are /your/rsem_results/prefix.genes.results and /your/rsem_results/prefix.isoforms.results. 






