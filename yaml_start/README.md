
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **yaml_start** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : yaml_start

Published in : 'yamldebugger: YAML parser debugger according to the QuantNet style guide. R package
version 0.5.0.'

Description : 'Shows the first steps how to install the yamldebugger package via
devtools::install_github and how to start the package and the help pages.'

Keywords : 'data mining, optimization, test, standardization, preprocessing, yaml, parser,
debugger, quantnet, style guide, package, github'

See also : yaml_run

Author : Lukas Borke

Submitted : 28.10.2016 by Lukas Borke

Example : Screenshot from the help pages of the yamldebugger package

```

![Picture1](yamldebugger_help_pages.png)


### R Code:
```r

# Clear all variables
rm(list = ls(all = TRUE))
graphics.off()


### STEP 0: install packages

## needed only for package installation or update

# The aim of 'devtools' is to make package development easier by providing R functions that simplify common tasks.
libraries = c("devtools")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
  install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)


## The devtools package provides install_github() that enables installing packages from GitHub.

# This command installs the yamldebugger package directly from GitHub,
# namely: https://github.com/lborke/yamldebugger
devtools::install_github("lborke/yamldebugger")


### STEP 1: once the yamldebugger package was installed you can start from this step everytime you want to debug new Quantlets

## load the package every time you want to use 'yamldebugger'
library(yamldebugger)

# Check if a keyword is in the Quantnet list
"plot" %in% allKeywords

# Check if several keywords are in the Quantnet list
c("time-series", "stochastic integration", "chi-square-test") %in% allKeywords


# start help pages for the main 4 functions of the yamldebugger package

help(yaml.debugger.init)

help(yaml.debugger.get.qnames)

help(yaml.debugger.run)

help(yaml.debugger.summary)

```
