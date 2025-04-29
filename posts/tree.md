---
layout: default
---

# Building a phylogenetic tree from MSA

Following up on building a [multiple sequence alignment](../basics/msa.md), a phylogenetic tree can be inferred and visualised. This short tutorial will work on a simple toy dataset using 4 betacoronavrius genomes (Accession numbers: AY597011, JX869059, MN908947, AY278491) retrieved from NCBI. See [this tutorial](../basics/ncbi_datasets.md) on how to retrieve them. This will cover inferrence of tree.

## Prerequisite 

* MAFFT
* IQTree

## Installation

```sh
conda install -c bioconda mafft iqtree
```

## Usage

1. Build the MSA

    Assuming your virus genomes are in a single fasta file called `virus.fna` 

    ```sh
    mafft --auto --thread 20 ./virus.fna > ./virus.msa.fna
    ```

    This will create a alignment file called `virus.msa.fna` in the same directory. Adjust the paths if necessary.

    *Note: In this example MSA of a whole virus genome is OK because they are relatively tiny. Of course it wouldn't be feasible to do such operation on genomes of larger size*

    *Note: Adjust the `--thread` parameters based on your setup.*

2. Infer the phylogenetic tree

    Optional: create a new directory to store your treefiles
    
    ```sh
    mkdir -pv ./treedir
    ```

    *Note: IQtree outputs a bunch of files at the end of the tree inference. It would be best to put them into a directory. Adjust the name `treedir` accordingly. It is always a good practice to include `-pv` in your `mkdir` command to prevent overriding existing directories.*

    ```sh
    iqtree -v -s ./virus.msa.fna --prefix treedir/virus_tree -B 1000 --boot-trees -T 20
    ```

    *Note: The `-B <INT>` adjusts the number of bootstraps with the minimum of 1000, along with `--boot-trees` flag, creates bootstrap of your phylogenetic tree. It is always ideal to do this step.* 

    *Note: Adjust the `-T` parameter for number of threads.*


    The directory of `treedir` will contain a multitude of files starting with the name as specified in the `--prefix` flag. Among those files, you will need the `prefix.contree` file, represeting a phylogenetic tree in newick format.

