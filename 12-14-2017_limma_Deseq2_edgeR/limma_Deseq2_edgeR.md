---
title: "limma_Deseq2_edgeR"
author: "Ruijuan Li"
date: "12/14/2017"
output: 
  html_document: 
    keep_md: yes
---

I was confused by the different protocols we used for expression analysis, Julin sometimes uses voom(), lmFit(), eBayes(), ... which seem to come from Limma pacakge, also there is vst transformation which is similar to log2 transformation. The protocol in edgeR is different from what Julin uses for some of his analysis. So I want to know what is the difference between different expression data analysis package: Limma/Deseq2/edgeR, and what is the difference between voom() and vst transformation, are they doing the same thing? What are their purposes? 

### Limma VS Deseq2 VS edgeR 
There are many papers comparing different tools for expression analysis. 
https://academic.oup.com/bib/article/16/1/59/240754 ... 
https://bmcbioinformatics.biomedcentral.com/track/pdf/10.1186/1471-2105-14-91?site=bmcbioinformatics.biomedcentral.com

* edgeR determines differential expression using empirical Bayes estimation and exact tests based on a negative binomial model. The package has been de- veloped to enable analysis of experiments with small numbers of replicates. In particular, an empirical Bayes procedure is used to moderate the degree of overdispersion across genes by borrowing informa- tion between genes. An exact test analogous to Fisher’s exact test but adapted to overdispersed data is used to assess differential expression for each gene. As default, the TMM normalization procedure is carried out to account for the different sequencing depths between the samples, whereas the Benjamini– Hochberg procedure is used to control the FDR [15].

* DESeq uses a similar negative binomial model as edgeR but models the observed relationship between the mean and variance when estimating dispersion, allowing a more general, data-driven par- ameter estimation. According to the method devel- opers, this allows a balanced selection of differentially expressed genes throughout the dynamic range of the data. Similar to edgeR, a scaling factor normal- ization procedure is carried out to account for the varying sequencing depths of the different samples and the Benjamini–Hochberg procedure is used to control the FDR. Also DESeq has been developed to enable analysis of experiments with small numbers of replicates. With DESeq, it is technically possible, although not recommended, to work with experi- ments without any biological replicates. 

* Limma: based on linear modeling. It was originally designed for analyzing microarray data but has recently been extended to RNA-seq data. The current recommendation according to the limma user guide is to use TMM normalization of the edgeR package and the so called ‘voom’- conversion which essentially transforms the normal- ized counts to logarithmic (base 2) scale and estimates their mean–variance relationship to determine a weight to each observation prior to linear modeling [20]. By default, the Benjamini–Hochberg proced- ure is used to estimate the FDR [15].

* My understanding 

1) Based on my understanding after reading different papers, there is no single good method for all different experiments. 

2) When the rep size is small, result should always be taken with caution, when the rep size is big, using which method does not matter that much. 

3) number of DEGs: DEsesq was often relatively conservative, while edgeR is too liberal (identify more DEGs), Limma performes well under many circumtances. (from Seyednasrollach et al. 2013), this result is basically consistent with finding from (Soenson and Delorenzi, 2013). 

4) true discovery rate etc.--- Deseq: low TPR (true positive rate), edgeR: generally high TPR, Limma: Low power for small sample sizes. Medium TPR for larger sample sizes 

I would like to know why Julin sometimes switch to Limma voom for expression analysis 

### Limma voom VS vst transformation for next time... 

I also have questions on large dispersion problem, and biological variation coeffcient, which I will explore next time. 
