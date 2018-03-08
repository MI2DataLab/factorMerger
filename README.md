# factorMerger: A Set of Tools to Support Adaptive Post-Hoc Fusing of Groups

[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/factorMerger)](https://cran.r-project.org/package=factorMerger)
[![Build Status](https://travis-ci.org/MI2DataLab/factorMerger.svg?branch=master)](https://travis-ci.org/MI2DataLab/factorMerger)
[![Pending Pull-Requests](http://githubbadges.herokuapp.com/MI2DataLab/factorMerger/pulls.svg)](https://github.com/MI2DataLab/factorMerger/pulls)
[![Github Issues](http://githubbadges.herokuapp.com/MI2DataLab/factorMerger/issues.svg)](https://github.com/MI2DataLab/factorMerger/issues)
[![DOI](https://zenodo.org/badge/70429809.svg)](https://zenodo.org/badge/latestdoi/70429809)

The aim of this project is to create an algorithm of post-hoc testing that would enable to extract hierarchical structure of factors with respect to a given response.

## Installing and loading `factorMerger`

`factorMerger` can be installed from [CRAN](https://cran.r-project.org/package=factorMerger) as follows:

```{r}
install.packages("factorMerger")
```

To install and load the latest version of`factorMerger` from **Github** run:

```{r}
devtools::install_github("MI2DataLab/factorMerger", build_vignettes = FALSE)
```

## Materials for `factorMerger`

A longer description of `factorMerger` may be found [here(https://arxiv.org/abs/1709.04412)](https://arxiv.org/abs/1709.04412).

[Cheatsheet, the pdf version](https://raw.githubusercontent.com/MI2DataLab/factorMerger/master/materials/factorMerger-cheatsheet.pdf)

![factorMerger cheatsheet](https://raw.githubusercontent.com/MI2DataLab/factorMerger/master/materials/factorMerger-cheatsheet.png)

## Working with `factorMerger`

<img src="https://raw.githubusercontent.com/MI2DataLab/factorMerger/master/README_workflow.png" alt="fm_workflow" width = '650'/>

### Examples

#### Survival analysis

```{r}
library(factorMerger)
library(forcats) # distinguish meaningful factors (fct_lump)

data("BRCA")
brcaSurv <- survival::Surv(time = BRCA$time, event = BRCA$vitalStatus)
drugName <- fct_lump(as.factor(BRCA$drugName), prop = 0.05) 

drugNameFM <- mergeFactors(response = brcaSurv[!is.na(drugName)], 
                           factor = drugName[!is.na(drugName)], 
                           family = "survival")

plot(drugNameFM, nodesSpacing = "effects", gicPanelColor = "grey2")

```


