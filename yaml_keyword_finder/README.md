
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **yaml_keyword_finder** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : yaml_keyword_finder

Published in : 'yamldebugger: YAML parser debugger according to the QuantNet style guide. R package
version 0.5.0.'

Description : 'Finds associations between a possible keyword and the document-term matrix DTM which
is extracted from the keywords in the YAML meta info in Quantlets. This might help the user to find
some correlated existing keywords from the Quantlets when the user is unsure which keywords should
be provided for the meta info of a new Quantlet.'

Keywords : 'data mining, correlation, optimization, test, standardization, preprocessing, yaml,
parser, debugger, quantnet, style guide, package, github'

See also : yaml_TDM_CorrPlot, yaml_keyword_frequency, yaml_wordcloud

Author : Lukas Borke

Submitted : 29.10.2016 by Lukas Borke

Example : 'Code example and output demonstrating how to find "similar" keywords for the given term
list with the keywords c("text-mining", "data-mining", "black-scholes", "distribution")'

```

### Example:
```r

> findAssocs(DTM, c("text-mining", "data-mining", "black-scholes", "distribution"), corlimit = c(0.3, 0.4, 0.5, 0.2) )
$`text-mining`
   data-adjustment data-visualization                lda 
              1.00               0.71               0.50 

$`data-mining`
data-adjustment   preprocessing 
           0.71            0.41 

$`black-scholes`
   option-price european-option            call          option 
           0.86            0.79            0.77            0.69 

$distribution
                cdf              normal                 pdf              cauchy             density normal-distribution 
               0.39                0.34                0.33                0.28                0.24                0.23 
             stable                 edf 
               0.22                0.21

```

### R Code:
```r

# Clear all variables
rm(list = ls(all = TRUE))
graphics.off()

# Install and load packages
libraries = c("tm")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
  install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)


(obj.names = load("yaml_DTM.RData", .GlobalEnv))

# summary of the DocumentTermMatrix containing the keywords from the YAML meta info in Quantlets
DTM


## Find associations in a document-term or term-document matrix.

# corlimit: a numeric vector (of the same length as terms; recycled otherwise) for the
# (inclusive) lower correlation limits of each term in the range from zero to one.

# The output is a named list. Each list component is named after a term in terms and contains a named numeric vector.
# Each vector holds matching terms from DTM and their rounded correlations satisfying the inclusive lower correlation limit of corlimit.

findAssocs(DTM, terms = "black-scholes", corlimit = 0.6)

findAssocs(DTM, "black-scholes", corlimit = 0.3)

findAssocs(DTM, "normal", corlimit = 0.3)

findAssocs(DTM, "normal-distribution", corlimit = 0.2)

findAssocs(DTM, "financial", corlimit = 0.3)

findAssocs(DTM, "text-mining", corlimit = 0.3)

findAssocs(DTM, "copula", corlimit = 0.3)


# Multiple associations: term vectors matched against DTM
findAssocs(DTM, c("text-mining", "data-mining", "black-scholes", "distribution"), corlimit = c(0.3, 0.4, 0.5, 0.2) )

findAssocs(DTM, c("time-series", "chart", "dax", "asset", "correlation"), corlimit = 0.2 )

```
