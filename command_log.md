# Quality control
fastqc salmonella_R1.fastq salmonella_R2.fastq -o fastqc_output/

# Trimming
trimmomatic PE \
  salmonella_R1.fastq salmonella_R2.fastq \
  salmonella_R1_paired.fq salmonella_R1_unpaired.fq \
  salmonella_R2_paired.fq salmonella_R2_unpaired.fq \
  SLIDINGWINDOW:4:20 MINLEN:50

# Assembly
spades.py -1 salmonella_R1_paired.fq -2 salmonella_R2_paired.fq -o spades_output/

# Filtering
seqkit seq -m 500 spades_output/contigs.fasta > filtered_contigs.fasta

# Assembly quality
quast.py filtered_contigs.fasta -o quast_output/

# Annotation
prokka filtered_contigs.fasta --outdir prokka_output/ --prefix salmonella

# AMR gene detection
amrfinder -n filtered_contigs.fasta -o amr_output.tsv

# MLST typing
mlst filtered_contigs.fasta > mlst_output.txt
