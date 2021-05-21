## Year 1 Sequencing Data

![White Logo](https://s3-us-west-2.amazonaws.com/human-pangenomics/backup/logo-proof-full.png)

*The [Human Pangenome Reference Consortium](https://humanpangenome.org/) produced sequencing data for assembly of 30 samples. Multiple data types including PacBio HiFi, Nanopore, Hi-C, and Bionano are avaiable. Strand-seq is available for 7 samples. Data created and hosted by the HPRC is open and available for download in our S3 & GCP buckets. Select data is also uploaded to international nucleotide sequencing databases (SRA/ENA/DDBJ) under the HPRC Genome Sequencing BioProject (PRJNA701308). 

For information about data reuse and publicating with HPRC data please see the HPRC's [Data Use Protocol](https://humanpangenome.org/data-use-protocol/). Note that the HPRC Year 1 data is pending publication, currently scheduled for mid-2021. If you would like to publish using this please contact the HPRC Coordinating Center at hprcadmin@gowustl.onmicrosoft.com.*

------------------

### Sequencing Data Production
* PacBio Hifi Data Produced By [UW](https://eichlerlab.gs.washington.edu/) and [WashU](https://www.genome.wustl.edu/)
* Hi-C Sequencing Data Produced By [UCSC](https://pgl.soe.ucsc.edu/)
* Strand-Seq Data Produced By [EMBL](https://www.embl.de/research/units/genome_biology/korbel/)
* Oxford Nanopore Data Produced By [UCSC](https://nanopore.soe.ucsc.edu/about)
* BioNano Data Produced By [Rockefeller](https://www.rockefeller.edu/research/vertebrate-genomes-project/vertebrate-genome-lab/)
* Karyotypes & Cell Line Microarray Data Produced By [Coriell](https://www.coriell.org/) and [CHOP](https://caglab.org/)

When available, the S3 and GCP buckets also include 1000G data (Illumina) for the trios from the [NYGC's](https://www.nygenome.org/) High Coverage dataset. This data was not generated for the HPRC, but was used for assembly and assembly QC.

------------------

### Data Layout
Data is sync'd between the AWS and GCP using [SSDS](https://github.com/DataBiosphere/ssds). Sequencing data is available in the working directory of the HPRC [S3](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=working/) and [GCP](https://console.cloud.google.com/storage/browser/fc-4310e737-a388-4a10-8c9e-babe06aaf0cf/working?authuser=0) buckets and is organized by each trios' child sample ID:
```
 ── working/
    ├── HPRC/
    │   └── HG00438/
    |       └── analysis/
    │           └── aligned_reads/
    │       └── assemblies/
    │       └── raw_data/
    │           └── Illumina/
    │           └── PacBio_HiFi/
    │           └── bionano/
    │           └── hic/
    │           └── karyotype/
    │           └── microarray/
    │           └── nanopore/     
    └── HPRC_PLUS/
        └── HG01442/
            └── analysis/        
            └── assemblies/
            └── raw_data/
```
AnVIL users can access the data stored in GCP through the public [AnVIL_HPRC workspace](https://app.terra.bio/#workspaces/anvil-datastorage/AnVIL_HPRC). Alternatively, data can be accessed directly from AWS or GCP, and data stored in the HPRC S3 Bucket can be accessed without egress fees.

### HPRC_PLUS
In addition to data produced by the HPRC, pre-existing datasets from external consortiums are included in the S3/GCP working trees under "HPRC_PLUS". These data include HG002 and HG005 from the [GIAB](https://www.nist.gov/programs-projects/genome-bottle) and HG00733 from the [HGSVC/1000G](https://www.internationalgenome.org/human-genome-structural-variation-consortium/). Publications resultant from the data listed under HPRC_PLUS which was produced by external consortiums should reference those consortiums or their original papers.

The table below provides a list of the samples included in the Year 1 Freeze. HPRC samples are in dark blue cells, and HPRC_PLUS samples are in light blue cells. 

![sample summary](https://s3-us-west-2.amazonaws.com/human-pangenomics/backup/Year1_Samples.png)

------------------

### PacBio HiFi Data From UW and WashU

PacBio HiFi sequencing was performed on the Sequel2 instrument using v2 chemistry. Samples were sequenced across 3-5 flowcells in order to generate 35-fold coverage or greater. The average coverage for the year1 samples is >40X with a median insert size of 20kb. The following file types are available:

* {flowcell_id}.ccs.bam - consensus called unaligned bam file
* {flowcell_id}.ccs.bam.md5 - md5 hash of ccs.bam file

Consensus sequences were generated with v4.0.0 of the CCS algorithm. Subreads files are available in the [backups area of the S3 bucket](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=backup/submissions/). 

HiFi reads aligned to GRCh38 and CHM13 with Winnowmap are included in samples' working tree under ```working/HPRC/{sample_id}/analysis/aligned_reads/hifi```. More information can be found in the README files for the algnments to [GRCh38](https://s3-us-west-2.amazonaws.com/human-pangenomics/submissions/93e97bf0-416a-11eb-b378-0242ac130002--WUSTL_Winnowmap_HiFi_Alignments_Y1Freeze/GRCh38/README) and [CHM13](https://s3-us-west-2.amazonaws.com/human-pangenomics/submissions/93e97bf0-416a-11eb-b378-0242ac130002--WUSTL_Winnowmap_HiFi_Alignments_Y1Freeze/CHM13v1Y/README). 

### Nanopore PromethION Data From UC Santa Cruz

The UCSC Nanopore PromethION HPP data were generated using the a new long read protocol (details to be published on protocols.io shortly). Briefly, this protocol uses Circulomics discs-based UHMW DNA isolation, followed by library preparation using ONT SQK-RAD004 kit and library cleanup using Circulomics discs. Typically, we used 3 RAD004-based sequencing libraries per PromethION flow cell (and 3 flow cells per individual). The observed read N50s (average) are ~80 kb, with 11x coverage in 100kb+ readsa dn 3x coverage in 200kb+ reads for each individual. The following file types are available: 
* sample.fast5.tar - signal data
* sample_Guppy_4.0.11_prom.fastq.gz - Fastq file basecalled using Guppy v4.0.11
* sample_Guppy_4.0.11_prom_sequencing_summary.txt.gz - Sequencing summary file from Guppy basecalling that can be used for indexing signal data
* sample_Guppy_4.0.11_prom.fused_reads.txt.gz - A catalog of reads that were found to be connected by Bulkvis (https://github.com/LooseLab/bulkvis) but artificially split by software. 

### Hi-C/Omni-C Data From UCSC

OmniC is a restriction enzyme-free HiC protocol. DNA is fragmented using an endonuclease that cuts DNA randomly, i.e., not at specific restriction sites. It uses a biotinylated linker to facilitate proximity ligation. This short linker sequence may be present within the read data. The architecture of an OmniC library molecule is:

P5adapter:GenomicRegion:Linker:GenomicRegion:P7adapter

Depending on the read length, some or all of the Linker sequence may be present in R1, R2, or both. When present, the Linker sequence is: 
```AGGTTCGTCCATCGATCGATGGACGAACCT``` 
Note that the linker sequence is a DNA palindrome. Thus, the Linker sequence will be the same whether present in R1 or R2 (forward or reverse read).


For each HPRC sample, two OmniC libraries are generated and sequenced. Duplicates can be identified and removed within each library, but not between libraries as independent sample material goes into each. Libraries are sequenced across several Novaseq lanes, depending on lane availability, with 2x150 paired-end sequencing.

The raw fastq OmniC data can be aligned using bwa mem with flags ```-5SP``` In practice, bwa mem (local alignment) will not omit the Linker sequence from the alignment in cases when it is present in the read.

Example alignment command:
```bwa mem -5SP <genome> <OmniC_R1.fq.gz> <OmniC_R2.fq.gz>```

The following file types are available:

* {library_name}.R1_001.fastq.gz - forward reads
* {library_name}.R2_001.fastq.gz - reverse reads

### Bionano Data From Rockefeller

The following file types are available:

* HG01361_Saphyr_DLE1_3680591.bnx.gz - raw data view of molecule and label information and quality scores
* HG01361_Saphyr_DLE1_3680616.cmap - location information for label sites
* MoleculeQualityReport.txt - summary report on molecular quality
* exp_informaticsReportSimple.txt - simple version of the exp_informaticsReport.txt file

For information about Bionano file specifications or utilization of Bionano files see [Bionano's website](https://bionanogenomics.com/support-page/data-analysis-documentation/).

### Strand-seq Data From EMBL

Strand-seq is a single-cell sequencing technology that resolves individual homologs within a cell by restricting sequence analysis to the DNA template strands used during DNA replication ([see Sanders, et al.](https://www.nature.com/articles/nprot.2017.029)). Strand-seq data is available for the following samples:

* HG01123
* HG01138
* HG01358
* HG01888
* HG01891
* HG02257
* HG02486

Each sample has 192 fastq.gz files available -- from paired-end sequencing of 96 single cells (nuclei).

### Trio Illumina Data From NYGC

When available, we have included high coverage (30X) Illumina datasets produced by NYGC for select 1000G samples. Information about this dataset can be found at [IGSR](https://www.internationalgenome.org/data-portal/data-collection/30x-grch38). 

Note that the data is stored in CRAM format (aligned to GRCHh38), but is placed in the raw_data area for each sample as the consortium uses the raw reads from the CRAMs. When used in assembly pipelines, the [extract_reads.wdl](https://github.com/human-pangenomics/hpp_production_workflows/blob/master/QC/wdl/tasks/extract_reads.wdl) is used to call ```samtools fastq``` to convert the reads to fastq format.

