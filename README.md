# RNAseq

**FASTQC**
```
/path/fastqc -t 3 myfile.fastq.gz --outdir=/path/OutputDir
```

**TRIMMOMATIC**

Single End
```
/path/trimmomatic-0.33.jar SE -threads 4 -phred33 -trimlog /path/LOG/myfile_log myfile.fastq.gz /path/OutputDir/myfile_trim.fastq.gz ILLUMINACLIP:/path/Trimmomatic-0.33/adapters/TruSeq3-SE.fa:2:30:10 HEADCROP:13
```

**KALLISTO**

Single End with pseudobams
```
/path/kallisto quant -i /path/IndexReference.idx -o /path/OutputDir --pseudobam --single -l 200 -s 20 myfile.fastq.gz | /path/samtools view -Sb - > /path/myfile_kallisto.bam
```

**BAMTOOLS**

>Sort a bam file
```
/path/samtools sort mybamfile.bam /path/OuputDir/mybamfile_sorted
```

>Create the index file of the bam
```
/path/samtools index mybamfile_sorted.bam
```

**PICARDTOOLS**

Mark duplicates
```
java -jar /path/MarkDuplicates.jar INPUT=mybamfile_sorted.bam OUTPUT=/path/OutputDir/mybamfile_sorted_picard.bam METRICS_FILE=/path/OutputDir/statsPicard.txt REMOVE_DUPLICATES=true TMP_DIR=/path/tmp
```

**SAMTOOLS**

Delete duplicates
```
/path/samtools rmdup -S mybamfile_sorted_picard.bam /path/OutputDir/mybamfile_sorted_picard_rmdup.bam
```




