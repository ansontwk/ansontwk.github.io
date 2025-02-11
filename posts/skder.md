---
layout: default
---

# Dereplicating genomes

Dereplicating genomes is a common step used in genomic analysis and in data cleaning. Redundant genomes are removed from a set of data so that the best genomes are selected as representative. Common tools are dRep, MASH and skDer.

I will be using the dataset retrieved from [this example](../basics/ncbi_datasets.md) as toy dataset, and dereplicating it into representative genomes using [skDer](https://github.com/raufs/skDER)

## Prerequisite 

* Conda

## Installation

```sh
conda create -n skder -c conda-forge -c bioconda skder
```

## Usage

1. Assuming your genomic assemblies/genomes are in a directory called `fna`, run

```sh
skder -g ./fna -o ./skder -l --threads 20
```

`-g` sets the input directory, `-o` sets the output directory. `-l` is optional that sets symbolic links in the output genomes instead of a direct copy. `--threads` sets number of threads to run skder. Bigger number good.

2. Give it some time

3. Your dereplicated genomes will be populated in the `Dereplicated_Representative_Genomes` subdirectory in the output path.

In the example, we started with 1603 genomes. After dereplication, we ended with 15 genomes. This corresponds to about 0.9% is representative, suggesting that the 1603 genomes may be very similar to each other.


*Note: You should probably shard and batch your genomes if you have more than 5000 genomes. The run time will increase signficantly as sample size increase since it's running pairwise comparisons.*

[back](../)