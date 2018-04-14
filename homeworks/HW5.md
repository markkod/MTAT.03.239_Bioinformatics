# Homework 5

## Task 1: Understanding linkage disequilibrium (1 point)
High linkage disequilibrium (LD) between genetic variants means that it is challenging to identify which of the many associated variants is the causal variant. One way to quantify LD between two genetic variants is to calculate the square of the Pearson's correlation coefficient (r<sup>2</sup>). Based on the genotype data presented in the [flow cytometry tutorial](https://github.com/kauralasoo/flow_cytomtery_genetics/blob/master/analysis/variance_components/estimate_variance_components.md),  estimate the number of genetic variants that are in high LD (r<sup>2</sup> > 0.8) with the lead CD14 QTL variant (rs778587). In your report, include the code that you used to calculate LD as well es the number of genetic variants with r<sup>2</sup> > 0.8 with rs778587. 

Note that the flow cytometry data is in its own GitHub repository: https://github.com/kauralasoo/flow_cytomtery_genetics.

## Task 2: Calculating empirical p-values (2 points)
One of the consequences of LD between genetic variants is that when we test associations between genetic variants and a phenotype, then it is difficult to accurately estimate how many independent tests are being performed. For example, in the [CD14 tutorial](https://github.com/kauralasoo/flow_cytomtery_genetics/blob/master/analysis/variance_components/estimate_variance_components.md), we tested the association between 541 genetic variants and CD14 expression. If the variants were all independent from each other, then we could use Bonferroni correction to correct for the number of test that we performed. However, as you can see from the Manhattan plot in the tutorial as well as from Task 1, many of the variants are in high LD with each other and therefore not independent. In this scenario, we could still use Bonferroni correction, but it is going to be over-conservation.

Alternatively, if we want to test if the smallest p-value observed in a region (such as in the region +/-200 kb from CD14 gene) is smaller than expected by chance, then instead of using Bonferroni correction, we can also use an empirical approach in which we permute the genotypes between individual multiple times, recalculate all correlations and then record the minimal p-value that we observed in the permuted data. By repeating this procedure multiple times (e.g. 100-10000), we can ask how often is the minimal p-value from permuted data smaller than than minimal p-value in our original dataset. If this is sufficiently rare then we conclude that our initial associations was statistically significant.

 1. Using the strategy described above, permute the labels (individuals) of the genotype dataset 100 times and redo the associations testing for CD14 expression using each of the permuted dataset. (HINT: `runMatrixEQTL` function has a `permute` flag that allows you to do that).
 2. From each permutation run, store the minimal association p-value across all tested variants. Finally, report report how often is the minimal p-value from the permutation runs smaller then the minimal p-value that you observed on the original dataset. Is the associations between CD14 cell surface expression rs778587 significant at 10% empirical FDR level?
 3. Repeat the same permutation analysis for CD16 and CD206 proteins. For both of these proteins, report how often is the minimal p-value from the permutation run smaller than the minimal p-value calculated on the original dataset. Are the associations that you detect for CD16 and CD206 statistically significant?
 
## Task 3: Understanding the mechanism of the CD14 QTL (2 points)
There are many possible ways how a genetic variant could change protein cell surface expression. One possibility is that the genetic variant changes the expression of the gene at the mRNA level and this in turn influences how much protein is made. Alternatively, the genetic variant could directly regulate the rate of protein translation or its stability with no effect on the mRNA. 
Can you find out, which of these two mechanisms is more likely to be true in the case of CD14 and rs778587? You can find the read counts of the CD14 gene from the [SummarizedExperiment object](https://courses.cs.ut.ee/2018/bioinfo/spring/uploads/Main/RNA_SummarizedExperiment.rds.zip) that you used in Homework 2. The genotypes for the rs778587 variant are available from [here](https://github.com/kauralasoo/flow_cytomtery_genetics/blob/master/data/genotypes/cd14_lead_variant.txt).  Use the read counts from the naive condition only. You can use linear regression (`lm` function in R) to test for the association between CD14 gene expression and rs778587 variant, but do not forget that you need to transform the read counts first (using either log transformation or variance stabilising transformation). Alternatively, you can also use the DESeq2 package. Illustrate your conclusions with a boxplots of CD14 gene and protein expression stratified by the genotype of the rs778587 variant.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NDQ3MjIxMV19
-->