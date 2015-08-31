# The number of SNPs per gene correlates with network degree 

#### By [Daniel Himmelstein](http://dhimmel.com) and [Casey Greene](http://www.greenelab.com/)

## Introduction

SNP to gene translation is a hallmark of modern bioinformatics. Genomic technologies often produce data on the nucleotide level. Downstream analyses, however, often operate on the gene level. Therefore, condensing nucleotide-level measurements to a gene-based value is a common and essential practice.

Many technologies and applications focus on single nucleotides that vary between individuals, which are called SNPs. Here, we investigate whether the number of SNPs contained by a gene is correlated with other types of gene centric information. Specifically, we evaluate whether the relationship between SNP abundance and network connectivity for a variety of network types.

When translating measurements from SNP to gene, a skilled bioinformatician will appreciate the correlations uncovered herein. Why? Gene scores from SNP-based experimentation are often analyzed in the context of other gene based information sources. Frequently, such analyses assume independence of the two datsets. However, if the SNP-to-gene conversion is biased by SNP abundance — which generally occurs absent painstaking consideration and adjustment — independence ceases to exist.

![](figure/degree-v-snps.png?raw=true)

![](figure/adj-degree-v-snps.png?raw=true)

![](figure/degree-v-snps-all.png?raw=true)

## Execution

This analysis can be reproduced by running the Jupyter notebooks in the following order:

1. [`network-degrees.ipynb`](network-degrees.ipynb) to extract gene degrees from [hetio-ind](https://github.com/dhimmel/integrate), a hetnet that includes many gene metaedges.
2. [`SNP-to-Gene.ipynb`](SNP-to-Gene.ipynb) to download data and perform processing for SNP chips.
3. [`exac.ipynb`](exac.ipynb) to process the [ExAC](http://exac.broadinstitute.org/) sequencing variants.
4. [`combine-SNPs-with-degrees.ipynb`](combine-SNPs-with-degrees.ipynb) to combine SNPs per Gene measurements from all platforms and hetnet degrees.
5. [`visualization.ipynb`](visualization.ipynb) to create visualizations. This is an [R notebook](https://github.com/IRkernel/IRkernel).
