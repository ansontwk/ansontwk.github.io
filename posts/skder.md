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

