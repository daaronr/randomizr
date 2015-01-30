<!-- README.md is generated from README.Rmd. Please edit that file -->
randomizr is designed to make conducting field, lab, survey, or online experiments easier by automating the random assignment process.

Installation from CRAN is easy:

``` r
install.packages("randomizr")
```

If you'd like to install the most current development release, use the following code:

``` r
install.packages("devtools")
devtools::install_github("acoppock/randomizr")
```

There are four functions in randomizr: simple\_ra(), complete\_ra(), block\_ra(), and cluster\_ra(), corresponding to common experimental designs.

complete\_ra() is the workhorse function that will be most appropriate for a large number of experimental situations: it assigns m of N units to treatment:

``` r
library(randomizr)
Z <- complete_ra(N=100, m=50)
table(Z)
#> Z
#>  0  1 
#> 50 50
```

A more complicated design that, for example, assigns different numbers of clusters to three different treatments can be accomodated like this:

``` r
# This makes a cluster variable: one unit in cluster "a", two in "b"...
clust_var <- rep(letters, times=1:26)

Z <- cluster_ra(clust_var=clust_var, m_each=c(7, 7, 12),
                condition_names=c("control", "placebo", "treatment"))
table(Z, clust_var)
#>            clust_var
#> Z            a  b  c  d  e  f  g  h  i  j  k  l  m  n  o  p  q  r  s  t  u
#>   control    0  0  0  0  5  6  0  8  0  0 11  0  0  0  0  0 17  0  0  0  0
#>   placebo    1  0  3  0  0  0  0  0  9  0  0  0 13  0 15  0  0  0  0  0 21
#>   treatment  0  2  0  4  0  0  7  0  0 10  0 12  0 14  0 16  0 18 19 20  0
#>            clust_var
#> Z            v  w  x  y  z
#>   control    0  0 24 25  0
#>   placebo   22  0  0  0  0
#>   treatment  0 23  0  0 26
```

Happy randomizing!
