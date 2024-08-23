### IASbreeding R Package

IASbreeding V0.1.0 can calculate kinship matrix, variance component analysis using linear mixed model, breeding value using BLUP. The core algorithm of IASbreeding is built using Rcpp and RcppEigen.

###	Install IAS-breeding software
Start an R session using RStudio and run these lines:  
```
install.packages("IASbreeding_0.1.0.zip", repos = NULL) 
install.packages("Rcpp","RcppEigen")
library(IASbreeding)
library(Rcpp)
library(RcppEigen)
```
****

###	How to using IAS-breeding software

+ Run BLUP

````
phe_file <- system.file("extdata", "Phenotype.txt", package = "IASbreeding", mustWork = TRUE)
pheno <- read.table(phe_file,header=TRUE)
ped_file <- system.file("extdata", "Pedigree.txt", package = "IASbreeding", mustWork = TRUE)
ped <- read.table(ped_file,header=TRUE)
newped<-pedcheck(ped)
A<-Akin(newped)
Results <- IASBLUP(BW56 ~ 1 + Sex + Condition,random = "ID", kinship = A, max_iter = 20, data = pheno)
````

+ Run GBLUP
```
bed_file <- system.file("extdata", "Genotype.bed", package = "IASbreeding", mustWork = TRUE)
file_prefix <- sub("\\.bed$", "", bed_file)
Genotype <-read_bed(file_prefix)
kin<-Gkin(Genotype)
Results <- IASBLUP(BW56 ~ 1 + Sex + Condition,random = "ID", kinship = kin, max_iter = 20, data = pheno)
```

+ Please read the instructions for the IAS-Breeding software for detailed usage.
