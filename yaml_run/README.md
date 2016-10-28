
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **yaml_run** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : yaml_run

Published in : 'yamldebugger: YAML parser debugger according to the QuantNet style guide. R package
version 0.5.0.'

Description : 'Shows how to run the yamldebugger package with the example of three existing
Quantlets. The interaction of the four main functions and the different aspects of the resulting
overview data structure are explained.'

Keywords : 'data mining, optimization, test, standardization, preprocessing, summary, yaml, parser,
debugger, quantnet, style guide, package, github'

See also : yaml_start

Author : Lukas Borke

Submitted : 28.10.2016 by Lukas Borke

Example : 'yamldebugger application on the example of three Quantlets in
https://github.com/QuantLet/Stochastic_processes'

```

### Example:
```r

## load the package every time you want to use 'yamldebugger'
library(yamldebugger)

> workdir = "c:/test"
> ## I: YAML initialization function: prepares and returns all data necesarry in the further process
> d_init = yaml.debugger.init(workdir, show_keywords = FALSE)
> ## II: Loads the list of Q folders. RootPath is required where the Qs are located.
> qnames = yaml.debugger.get.qnames(d_init$RootPath)
[1] "3 Q folder(s) found:"
[1] "ar1_process"    "random_walk"    "randomwalk_ar1"
> ## III: Main part of the YAML debugger. Loops trough the provided Q folders and extracts YAML meta info.
> # If errors occur, corresponding error handling is executed.
> d_results = yaml.debugger.run(qnames, d_init)
[1] "1: ar1_process"
[1] "--------------------------------------------------------------------"
[1] "2: random_walk"
[1] "--------------------------------------------------------------------"
[1] "3: randomwalk_ar1"
[1] "--------------------------------------------------------------------"
> ## IV: Overview of the parser results. If errors occured, the corresponding Q names and YAML errors are displayed.
> OverView = yaml.debugger.summary(qnames, d_results, summaryType = "mini")
> 
> OverView
     Q Names          Missing Style Guide fields Descriptions stats             Keywords stats               
[1,] "ar1_process"    ""                         "32 word(s), 157 Character(s)" "NA: 9 (standard), NA (new)" 
[2,] "random_walk"    ""                         "17 word(s), 93 Character(s)"  "NA: 9 (standard), NA (new)" 
[3,] "randomwalk_ar1" ""                         "58 word(s), 273 Character(s)" "NA: 12 (standard), NA (new)"

```

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

# Application example. Make sure you have some Q folders on your lokal disk for validating.
# Let 'workdir' be the folder where the Q folders are stored.
# You can take three Quantlet examples from the subfolder 'examples' of this Quantlet, put them into any lokal folder of your computer
# and adjust the parameter 'workdir' if necesarry.

workdir = "c:/test"
# workdir = "c:/.../examples"

## I: YAML initialization function: prepares and returns all data necesarry in the further process
d_init = yaml.debugger.init(workdir, show_keywords = TRUE)
# d_init = yaml.debugger.init(workdir, show_keywords = FALSE)

## II: Loads the list of Q folders. RootPath is required where the Qs are located.
qnames = yaml.debugger.get.qnames(d_init$RootPath)

## III: Main part of the YAML debugger. Loops trough the provided Q folders and extracts YAML meta info.
# If errors occur, corresponding error handling is executed.
d_results = yaml.debugger.run(qnames, d_init)

## IV: Overview of the parser results. If errors occured, the corresponding Q names and YAML errors are displayed.
OverView = yaml.debugger.summary(qnames, d_results, summaryType = "mini")

OverView = yaml.debugger.summary(qnames, d_results, summaryType = "compact")

OverView = yaml.debugger.summary(qnames, d_results, summaryType = "full")

# 'yaml.debugger.summary' provides 3 levels of detail : "mini", "compact", "full"

## You can also access the OverView structure via the variable 'OverView'

dim(OverView)

OverView

OverView[1,]

OverView[,1]

```
