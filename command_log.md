### 🔬 **1. Quality Control**

Use **FastQC** to assess the quality of raw sequencing reads:

```bash
fastqc salmonella_R1.fastq salmonella_R2.fastq
```

---

### ✂️ **2. Trimming**

Use **Trimmomatic** to remove low-quality bases and adapters:

```bash
trimmomatic PE \
  salmonella_R1.fastq salmonella_R2.fastq \
  salmonella_R1_paired.fq salmonella_R1_unpaired.fq \
  salmonella_R2_paired.fq salmonella_R2_unpaired.fq \
  SLIDINGWINDOW:4:20 MINLEN:50
```

---

### 🧬 **3. Genome Assembly**

Use **SPAdes** for de novo assembly of the trimmed, paired-end reads:

```bash
spades.py -1 salmonella_R1_paired.fq -2 salmonella_R2_paired.fq
```

---

### 🔍 **4. Contig Filtering**

Use **SeqKit** to retain only contigs ≥500 bp:

```bash
seqkit seq -m 500 spades_output/contigs.fasta > filtered_contigs.fasta
```

---

### 📊 **5. Assembly Quality Check**

Use **QUAST** to evaluate assembly metrics:

```bash
quast.py filtered_contigs.fasta -o quast_output/
```

---

### 🧬 **6. Genome Annotation**

Use **Prokka** to annotate genes in the filtered contigs:

```bash
prokka filtered_contigs.fasta --outdir prokka_output/ --prefix salmonella
```

---

### 🧫 **7. AMR Gene Detection**

Use **AMRFinderPlus** to identify antimicrobial resistance genes:

```bash
amrfinder -n filtered_contigs.fasta -o amr_output.tsv
```

---

Would you like this turned into a **Nextflow** pipeline or a **flowchart diagram** for documentation or presentation?
