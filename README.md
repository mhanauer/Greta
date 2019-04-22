---
title: "FHHC Report"
output:
  pdf_document: default
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Different installations that I have tried
```{r}
#install_tensorflow(extra_packages = "tensorflow-probability")
#tensorflow::install_tensorflow(version = "1.11.0", extra_packages = "tensorflow-probability")
#install_tensorflow(method = "auto")
#reticulate::conda_install("r-tensorflow", "tensorflow-probability", pip = TRUE)
#devtools::install_github("greta-dev/greta")
#reticulate::virtualenv_remove("r-tensorflow")
```

Greta
```{r}
library(igraph)
library(DiagrammeR)
library(reticulate)
install.packages("installr")
devtools::install_github('talgalili/installr')
library(installr)
uninstall.packages("greta")
remove.packages("greta")
remove.packages("reticulate")
uninstall.packages("reticulate")
devtools::install_github("rstudio/reticulate", force = TRUE)
library(reticulate)
install_tensorflow(method = "conda")
```
Try example
```{r}
#devtools::install_github("greta-dev/greta", force = TRUE)
library(greta)
x <- as_data(iris$Petal.Length)
y <- as_data(iris$Sepal.Length)


# variables and priors
int <- normal(0, 1)
coef <- normal(0, 3)
sd <- student(3, 0, 1, truncation = c(0, Inf))

# operations
mean <- int + coef * x
distribution(y) <- normal(mean, sd)
m <- model(int, coef, sd)
plot(m)

draws <-  mcmc(m, n_samples = 1000, warmup = 1000, chains = 4)
draws
summary(draws)
sessionInfo()
```




