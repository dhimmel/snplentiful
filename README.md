# The number of SNPs per gene correlates with network degree 

## By [Daniel Himmelstein](http://dhimmel.com) and [Casey Greene](http://www.greenelab.com/)

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
