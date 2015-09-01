# The number of SNPs per gene correlates with network degree 

#### By [Daniel Himmelstein](http://dhimmel.com) and [Casey Greene](http://www.greenelab.com/)

## Introduction

SNP to gene translation is a hallmark of modern bioinformatics. Genomic technologies often produce data on the nucleotide level. Downstream analyses, however, often operate on the gene level. Therefore, condensing nucleotide-level measurements to a gene-based value is a common and essential practice.

Many technologies and applications focus on single nucleotides that vary between individuals, which are called SNPs. Here, we investigate whether the number of SNPs contained by a gene is correlated with other types of gene centric information. Specifically, we evaluate the relationship between SNP abundance and network connectivity for a variety of network types.

When translating measurements from SNP to gene, a skilled bioinformatician will appreciate the correlations uncovered herein. Why? Gene scores from SNP-based experimentation are often analyzed in the context of other gene based information sources. Frequently, such analyses assume independence of the two datasets. However, if the SNP-to-gene conversion is biased by SNP abundance — which generally occurs absent painstaking consideration and adjustment — independence ceases to exist.

## Method

**SNP abundance:** We calculated the number of SNPs per gene for 3 genotyping arrays ([Affymetrix 500K Set](http://www.affymetrix.com/catalog/131459/AFFY/Mapping+500K+Array+Set), [Illumina HumanHap550](https://support.illumina.com/array/array_kits/humanhap550-quad_plus_dna_analysis_kit.html), [Illumina HumanOmni1](https://support.illumina.com/array/array_kits/humanomni1-quad_beadchip_kit.html)), exome sequencing ([ExAC](http://exac.broadinstitute.org/)), and whole genome sequencing ([1000 Genomes Phase 3](http://www.1000genomes.org/announcements/initial-phase-3-variant-list-and-phased-genotypes-2014-06-24)). We limited analyses to [genes](https://dx.doi.org/10.6084/m9.figshare.103113) that were [consistent](http://www.gettinggeneticsdone.com/2011/06/mapping-snps-to-genes-for-gwas.html) between databases and extended each gene boundary by 10,000 basepairs in both directions. The 10,000 basepair window is frequently adopted to capture unmeasured but highly linked SNPs underlying the association and to cover nearby regulatory variants.

**Network degree:** Hetnets are networks with multiple types of nodes and edges. We extracted gene degrees from [hetio-ind](http://dx.doi.org/10.15363/thinklab.d102), a hetnet developed for drug repurposing. The network contained [26 types of edges](download/network-summary.tsv) (metaedges) that originate with a gene. Thus, for each gene we calculated 26 metaedge-specific degrees.

**Transformation:** Both SNP abundances and network degrees were transformed by adding 1 and taking the logarithm with base 10. Figure axes report untransformed values, but model fitting occurs on the tranformed data.

## Results

Correlations between SNP abundance and network degree are commonplace. These correlations affect genotyping arrays as well as sequencing indicating that effects are not solely due to biased coverage of genotyping arrays. Physical protein interactions — a popular input for GWAS prioritization techniques — shows less correlation than other types. However, GO annotations — a community favorite for gene set enrichment techniques — increase sharply with SNP abundance. Expression datasets also preferentially report genes with high SNP abundance.

## Conclusions

Beware! The potential for erroneous conclusions when gene scores are biased by SNP abundance is high. Ideally, permutation testing should be applied on the SNP level to ensure that SNP to gene conversion biases are not the cause of any positive results. Since access to the raw SNP level data needed for permutation is often impractical or unavailable, care should be taken to use unbiased SNP to gene conversion methods.

## Figures

<a name="fig1"></a>
![The number of SNPs in a gene varies with network degree](figure/degree-v-snps.png)
**Figure 1: Network degree versus SNP abundance for common data types.** Platform and metaedge specific models were fit. Models are drawn as their 95% confidence band. The genes with extreme SNP abundances (bottom and two two percentiles) are omitted for visual clarity.

<a name="fig2"></a>
![The number of SNPs in a gene varies with network degree](figure/adj-degree-v-snps.png)
**Figure 2: Mean-adjusted network degree versus SNP abundance for common data types.** The same as [Figure 1](#fig1) except that degree was divided by the mean degree for each metaedge.

<a name="fig3"></a>
![The number of SNPs in a gene varies with network degree](figure/degree-v-snps-all.png)
**Figure 3: Network degree versus SNP abundance for all metaedges.** The same as [Figure 1](#fig1) except that all metaedges with over 1,000 edges are shown. Additionally, genes with extreme SNP abundances were not removed. See [`download/network-summary.tsv`](download/network-summary.tsv) for abbreviation lookup and additional metaedge information.

## Execution

This analysis can be reproduced by running the Jupyter notebooks in the following order:

1. [`network-degrees.ipynb`](network-degrees.ipynb) to extract gene degrees from [hetio-ind](https://github.com/dhimmel/integrate), a hetnet that includes many gene metaedges.
2. [`SNP-to-Gene.ipynb`](SNP-to-Gene.ipynb) to download data and perform processing for SNP chips.
3. [`exac.ipynb`](exac.ipynb) to process the [ExAC](http://exac.broadinstitute.org/) sequencing variants.
4. [`combine-SNPs-and-degrees.ipynb`](combine-SNPs-and-degrees.ipynb) to combine SNPs per Gene measurements from all platforms and hetnet degrees.
5. [`visualization.ipynb`](visualization.ipynb) to create visualizations. This is an [R notebook](https://github.com/IRkernel/IRkernel).
