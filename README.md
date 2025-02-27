[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bactopia/bactopia)](https://github.com/bactopia/bactopia/releases)
[![Anaconda-Server Badge](https://anaconda.org/bioconda/bactopia/badges/installer/conda.svg)](https://bioconda.github.io/recipes/bactopia/README.html) 
[![Anaconda-Server Badge](https://anaconda.org/bioconda/bactopia/badges/downloads.svg)](https://anaconda.org/bioconda/bactopia)
![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bactopia/bactopia/bactopia-commands)
[![mSystems](https://img.shields.io/badge/DOI-mSystems.00190--20-blue)](https://doi.org/10.1128/mSystems.00190-20)
[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-908a85?logo=gitpod)](https://gitpod.io/#https://github.com/bactopia/bactopia)

![Bactopia Logo](data/bactopia-logo.png)

# Bactopia
Bactopia is a flexible pipeline for complete analysis of bacterial genomes. The goal of Bactopia is to process your data with a broad set of tools, so that you can get to the fun part of analyses quicker!

Bactopia can be split into three main parts: [Bactopia Datasets](https://bactopia.github.io/datasets/), [Bactopia Analysis Pipeline](https://bactopia.github.io/#bactopia-workflow), and [Bactopia Tools](https://bactopia.github.io/bactopia-tools/).

![Bactopia Overview](data/bactopia-overview.png)

Bactopia Datasets provide a framework for including many existing public datasets, as well as private datasets, into your analysis The process of downloading, building, and (or) configuring these datasets for Bactopia has been automated.

Bactopia Analysis Pipeline is the main *per-isolate* workflow in Bactopia. Built with  [Nextflow](https://www.nextflow.io/), input FASTQs (local or available from SRA/ENA) are put through numerous analyses including: quality control, assembly, annotation, reference mapping, variant calling, minmer sketch queries, blast alignments, insertion site prediction, sequence typing, and more. The Bactopia Analysis Pipeline automatically selects which analyses to include based on the available Bactopia Datasets.

![Bactopia Overview](data/bactopia-workflow.png)

Bactopia Tools are a set a independent workflows for comparative analyses. The comparative analyses may include summary reports, pan-genome, or phylogenetic tree construction. Using the [predictable output structure](https://bactopia.github.io/output-overview/) of Bactopia you can pick and choose which samples to include for processing with a Bactopia Tool.

Bactopia was inspired by [Staphopia](https://staphopia.emory.edu/), a workflow we (Tim Read and myself) released that targets *Staphylococcus aureus* genomes. Using what we learned from Staphopia and user feedback, Bactopia was developed from scratch with usability, portability, and speed in mind from the start.

# Documentation
Documentation for Bactopia is available at https://bactopia.github.io/. The documentation includes a tutorial replicating [Staphopia](https://staphopia.emory.edu) and a complete overview of Bactopia. I highly encourage you check it out!

# Quick Start
```
mamba create -y -n bactopia -c conda-forge -c bioconda bactopia
conda activate bactopia
bactopia datasets

# Paired-end
bactopia --R1 R1.fastq.gz --R2 R2.fastq.gz --sample SAMPLE_NAME \
         --datasets datasets/ --outdir OUTDIR

# Single-End
bactopia --SE SAMPLE.fastq.gz --sample SAMPLE --datasets datasets/ --outdir OUTDIR

# Multiple Samples
bactopia prepare MY-FASTQS/ > fastqs.txt
bactopia --fastqs fastqs.txt --datasets datasets --outdir OUTDIR

# Single ENA/SRA Experiment
bactopia --accession SRX000000 --datasets datasets --outdir OUTDIR

# Multiple ENA/SRA Experiments
bactopia search "staphylococcus aureus" > accessions.txt
bactopia --accessions accessions.txt --dataset datasets --outdir ${OUTDIR}
```

# Installation
Bactopia has **a lot** of tools built into its workflow. As you can imagine, all these tools lead to numerous dependencies, and navigating dependencies can often turn into a very frustrating process. With this in mind, from the onset Bactopia was developed to only include programs that are installable using [Conda](https://conda.io/en/latest/).

Conda is an open source package management system and environment management system that runs on Windows, macOS and Linux. In other words, it makes it super easy to get the tools you need installed! The [official Conda documentation](https://conda.io/projects/conda/en/latest/user-guide/install/index.html) is a good starting point for getting started with Conda. Bactopia has been tested using the [Miniconda installer](https://conda.io/en/latest/miniconda.html), but the [Anaconda installer](https://www.anaconda.com/distribution/) should work the same.

Once you have Conda all set up, you are ready to create an environment for Bactopia. I personally recommend you used [mamba](https://github.com/mamba-org/mamba) (_soooo fast!_) to install Bactopia, but either of these commands should work:

```
# Recommended
mamba create -n bactopia -c conda-forge -c bioconda bactopia

# or with standard conda
conda create -n bactopia -c conda-forge -c bioconda bactopia
```

After a few minutes you will have a new conda environment suitably named *bactopia*. To activate this environment, you will can use the following command:

```
conda activate bactopia
```

And voilà, you are all set to get started processing your data!

# Please Cite Datasets and Tools
If you have used Bactopia in your work, please be sure to cite any datasets or tools you may have used. [A list of each dataset/tool used by Bactopia has been made available](https://bactopia.github.io/acknowledgements/). 

*If a citation needs to be updated please let me know!*

# Acknowledgements
Bactopia is truly a case of *"standing upon the shoulders of giants"*. Nearly every component of Bactopia was created by others and made freely available to the public.

I would like to personally extend my many thanks and gratitude to the authors of these software packages and public datasets. If you've made it this far, I owe you a beer 🍻 (or coffee ☕!) if we ever encounter one another in person. Really, thank you very much!

# Alternatives
In case Bactopia doesn't fit your needs, here are some alternatives you can checkout. I personally haven't used them, but you might find them to fit your needs! If you ran into issues using Bactopia, please feel free to [reach out](https://github.com/bactopia/bactopia/issues/new/choose)!

* __[AQUAMIS](https://gitlab.com/bfr_bioinformatics/AQUAMIS)__  
Deneke C, Brendebach H, Uelze L, Borowiak M, Malorny B, Tausch SH. *Species-Specific Quality Control, Assembly and Contamination Detection in Microbial Isolate Sequences with AQUAMIS.* __Genes__. 2021;12. doi:10.3390/genes12050644

* __[ASA³P](https://github.com/oschwengers/asap)__  
Schwengers O, Hoek A, Fritzenwanker M, Falgenhauer L, Hain T, Chakraborty T, Goesmann A. *ASA³P: An automatic and scalable pipeline for the assembly, annotation and higher-level analysis of closely related bacterial isolates.* __PLoS Comput Biol__ 2020;16:e1007134. https://doi.org/10.1371/journal.pcbi.1007134.

* __[MicroPIPE](https://github.com/BeatsonLab-MicrobialGenomics/micropipe)__  
Murigneux V, Roberts LW, Forde BM, Phan M-D, Nhu NTK, Irwin AD, Harris PNA, Paterson DL, Schembri MA, Whiley DM, Beatson SA *MicroPIPE: validating an end-to-end workflow for high-quality complete bacterial genome construction.* __BMC Genomics__, 22(1), 474. (2021) https://doi.org/10.1186/s12864-021-07767-z

* __[Nullarbor](https://github.com/tseemann/nullarbor)__  
Seemann T, Goncalves da Silva A, Bulach DM, Schultz MB, Kwong JC, Howden BP. *Nullarbor* __Github__ https://github.com/tseemann/nullarbor 

* __[ProkEvo](https://github.com/npavlovikj/ProkEvo)__  
Pavlovikj N, Gomes-Neto JC, Deogun JS, Benson AK *ProkEvo: an automated, reproducible, and scalable framework for high-throughput bacterial population genomics analyses.* __PeerJ__, e11376 (2021) https://doi.org/10.7717/peerj.11376

* __[Public Health Bacterial Genomics](https://github.com/theiagen/public_health_bacterial_genomics)__  
Libuit K, Ambrosio F, Kapsak C *Public Health Bacterial Genomics* __GitHub__ https://github.com/theiagen/public_health_bacterial_genomics

* __[rMAP](https://github.com/GunzIvan28/rMAP)__  
Sserwadda I, Mboowa G *rMAP: the Rapid Microbial Analysis Pipeline for ESKAPE bacterial group whole-genome sequence data.* __Microbial Genomics__, 7(6). (2021) https://doi.org/10.1099/mgen.0.000583

* __[TORMES](https://github.com/nmquijada/tormes)__  
Quijada NM, Rodríguez-Lázaro D, Eiros JM, Hernández M. *TORMES: an automated pipeline for whole bacterial genome analysis.* __Bioinformatics__ 2019;35:4207–12. https://doi.org/10.1093/bioinformatics/btz220.

# Feedback
Your feedback is very valuable! If you run into any issues using Bactopia, have questions, or have some ideas to improve Bactopia, I highly encourage you to submit it to the [Issue Tracker](https://github.com/bactopia/bactopia/issues).

# License
[MIT License](https://raw.githubusercontent.com/bactopia/bactopia/master/LICENSE)

# Citation
Petit III RA, Read TD, *Bactopia: a flexible pipeline for complete analysis of bacterial genomes.* __mSystems__. 5 (2020), https://doi.org/10.1128/mSystems.00190-20.

# Author 

* Robert A. Petit III
* Twitter: [@rpetit3](https://twitter.com/rpetit3)
