# [StatQuest: A gentle introduction to RNA-seq](https://www.youtube.com/watch?v=tlf6wYJrwKY&list=PLf-FWZiYNojtbpEDgn1LCzhaSVFdA-BjD)

* High throughput sequencing tells us which genes are active & how much they are transcribed.

    * High-throughput sequencing specifically refers to sequencing techniques like Illumina that allow you to sequence massive amounts of DNA at once means hundreds of thousands of strands.

* 3 main steps for RNA-Seq

    1. Prepare a Sequencing Library
    2. Sequence
    3. Data Analysis

* Prepare a Sequencing Library (Illumina protocol and sequencer)

    1. Isolate RNA
    2. Break RNA into smaller fragments (Bcoz the sequencing machine needs short fragments)
    3. Convert the RNA into double stranded DNA (Bcoz dsDNA is more stable and can be easily modified and amplified)
    4. Add Sequencing Adaptors (Bcoz they allow sequencing maching to recognize the fragments & can be used to sequence different samples at the same time by using different adaptors for each sample)
    5. PCR amplify (only fragments with adaptors are amplified, enriched)
    6. QC - Verify library concentration & library fragment lengths (Not too long or short)

* Sequence the Library

    * Fragments are laid out vertically in a grid (Flow Cell) in the Sequencer
    * The Machine has color coded fluroscent probes (different colour for each nucleotide)
    * The probes are attached to first base from bottom, a picture is taken and the fluroscent thing is washed of the probe
    * similarly now the probe is attached to next base and so on
    * Quality Score, reflects how confident the machine is for a particular base
    * Low Diversity (same type of colour in a region) results in low quality score as it will make it hard to identify the individual sequences (they will blur together), this is especially a problem when the first few nucleotides are sequenced as that is when we locate the fragments on the grid.

* Raw Data
    * Each read consists of 4 lines of data
    * The first line starts with '@', is the unique identifier for the sequence
    * The second line contains the actual sequence of bases.
    * The third line always contains '+' (why?)
    * The fourth line contains quality scores for each base in the read

* Raw Data processing
    * Filter out the garbage reads
    * Align the high quality reads to the genome
    * Count the number of reads per gene

* Filter out the Garbage reads
    * Low quality reads
    * Artifacts of chemestry (Adaptor bound with another Adaptor is a garbage read)

* Aligning to Genome
    * Break the Genome & Read into fragments (while indexing and storing their location) & align them
    * We break them into fragments bcoz intra-species variation will cause no alignment otherwise


* Count the number of reads per gene    
    * Check the Gene location from records and compare with the locations of reads
    * Count the number of reads per gene


* Bulk RNA-Seq, where a sample is the average of a pool of cells (6 million) - low total sample size (around 6)
* Single Cell RNA-Seq trats each sample like and individual cell, so it can generate a lot of samples (around 800)

* Normalize for the total Reads in each sample.

* Data Analysis
    1. Plot the Data using PCA 
        * PCA reduces the number of axes you need to display the important aspects of the data
        * Tells us if we can expect to find interesting differences
        * Tells us if we should some samples (outliers) from any down stream analysis

    2. Identify differentially expressed genes between normal & mutant samples
        * Done using edgeR & DESeq2 (?)
        * logFC (Fold Change - how big the relative difference between normal & tumour) - Y axis
        * logCPM (Counts per miillion, is a type of normalization, tells about transcription, going right increases) - X axis
        * Red dots mean there is differential expression for that particular gene while black means - no difference 

    3. Now what?
        * If you know what you are looking for, you can see if the experiment validated your hypothesis
        * Otherwise, you can see if certain pathways are enriched in either the normal or mutant gene sets