
<!-- README.md is generated from README.Rmd. Please edit that file -->

# CHD (Congenital Heart Disease) codes

<!-- badges: start -->
<!-- badges: end -->

This repository contains the SNOMED codes referred to in the NHSR
Community webinar [Unveiling Congenital Heart Disease and Comorbidities
using Primary Care
data](https://www.youtube.com/embed/vSekPvgwJKY?si=1a9OpLPIwGE6Fkhj)
presented by James Partington on 10 July 2024.

The data is an extract of the SNOMED reference page from the CHD Power
BI tool developed by the Cheshire and Merseyside Health and Care
Partnership in conjunction with the Cheshire CHD in Primary Care Group
and shared with kind permission from James Partington and colleagues.

Copyright: Cheshire and Wirral Partnership NHS Foundation Trust,
Cheshire and Merseyside Health and Care Partnership

The full list of codes in the csv has been provided to the CHD Clinical
Reference Group and is subject to their ongoing review, plus ongoing
review by the Cheshire CHD in Primary Care Group

To import this csv file into R:

``` r
library(readr)
library(janitor) # cleans the column names by removing spaces and makes all lower case
#> 
#> Attaching package: 'janitor'
#> The following objects are masked from 'package:stats':
#> 
#>     chisq.test, fisher.test

chd_codes <- read_csv("data/chd-codes.csv", 
    col_types = cols(`SNOMED Concept ID` = col_character())) |> 
    clean_names()
```

Note that the column `SNOMED Concept ID` (converted with the janitor
package to `snomed_concept_id`) is recognised by R as a number so
appears in scientific notation. The code above sets the ID to character
so all the characters show.

If you wish to have this column as numbers use the following dplyr code:

``` r
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union

chd_codes <- chd_codes |> 
  mutate(snomed_concept_id_formatted = as.numeric(snomed_concept_id))
```
