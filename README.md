---
title: "FHHC Report"
output:
  pdf_document: default
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Greta
```{r}
#install_tensorflow(method = "auto")
#reticulate::conda_install("r-tensorflow", "tensorflow-probability", pip = TRUE)
library(greta)
library(igraph)
library(DiagrammeR)
```
Try example
```{r}
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
install.packages("greta")
devtools::install_github("greta-dev/greta")
install_tensorflow(extra_packages = "tensorflow-probability")
library(greta)
draws <-  mcmc(m, n_samples = 1000, warmup = 1000, chains = 4)
draws
summary(draws)
```




