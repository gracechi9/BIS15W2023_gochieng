---
title: "Lab 3 Homework"
author: "Grace Ochieng"
date: "2023-01-17 "
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
help("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## No documentation for 'data/mammals_sleep_allison_cicchetti_1976.csv' in specified packages and libraries:
## you could try '??data/mammals_sleep_allison_cicchetti_1976.csv'
```

```r
getwd()
```

```
## [1] "/Users/achichi/Desktop/BIS15W2023_gochieng clone/lab3"
```

2. Store these data into a new data frame `sleep`.

```r
sleep <- readr::read_csv("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 62 11
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  


```r
anyNA(sleep)
```

```
## [1] FALSE
```

5. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body weight in kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```

```r
str(sleep)
```

```
## spc_tbl_ [62 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ species                                                        : chr [1:62] "African elephant" "African giant pouched rat" "Arctic Fox" "Arctic ground squirrel" ...
##  $ body weight in kg                                              : num [1:62] 6654 1 3.38 0.92 2547 ...
##  $ brain weight in g                                              : num [1:62] 5712 6.6 44.5 5.7 4603 ...
##  $ slow wave ("nondreaming") sleep (hrs/day)                      : num [1:62] -999 6.3 -999 -999 2.1 9.1 15.8 5.2 10.9 8.3 ...
##  $ paradoxical ("dreaming") sleep (hrs/day)                       : num [1:62] -999 2 -999 -999 1.8 0.7 3.9 1 3.6 1.4 ...
##  $ total sleep (hrs/day)  (sum of slow wave and paradoxical sleep): num [1:62] 3.3 8.3 12.5 16.5 3.9 9.8 19.7 6.2 14.5 9.7 ...
##  $ maximum life span (years)                                      : num [1:62] 38.6 4.5 14 -999 69 27 19 30.4 28 50 ...
##  $ gestation time (days)                                          : num [1:62] 645 42 60 25 624 180 35 392 63 230 ...
##  $ predation index (1-5)                                          : num [1:62] 3 3 1 5 3 4 1 4 1 1 ...
##  $ sleep exposure index (1-5)                                     : num [1:62] 5 1 1 2 5 4 1 5 2 1 ...
##  $ overall danger index (1-5)                                     : num [1:62] 3 3 1 3 4 4 1 4 1 1 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   species = col_character(),
##   ..   `body weight in kg` = col_double(),
##   ..   `brain weight in g` = col_double(),
##   ..   `slow wave ("nondreaming") sleep (hrs/day)` = col_double(),
##   ..   `paradoxical ("dreaming") sleep (hrs/day)` = col_double(),
##   ..   `total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)` = col_double(),
##   ..   `maximum life span (years)` = col_double(),
##   ..   `gestation time (days)` = col_double(),
##   ..   `predation index (1-5)` = col_double(),
##   ..   `sleep exposure index (1-5)` = col_double(),
##   ..   `overall danger index (1-5)` = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

6. How many herbivores are represented in the data?  

```r
table(sleep$species)
```

```
## 
##          African elephant African giant pouched rat                Arctic Fox 
##                         1                         1                         1 
##    Arctic ground squirrel            Asian elephant                    Baboon 
##                         1                         1                         1 
##             Big brown bat           Brazilian tapir                       Cat 
##                         1                         1                         1 
##                Chimpanzee                Chinchilla                       Cow 
##                         1                         1                         1 
##           Desert hedgehog                    Donkey     Eastern American mole 
##                         1                         1                         1 
##                   Echidna         European hedgehog                    Galago 
##                         1                         1                         1 
##                     Genet           Giant armadillo                   Giraffe 
##                         1                         1                         1 
##                      Goat            Golden hamster                   Gorilla 
##                         1                         1                         1 
##                 Gray seal                 Gray wolf           Ground squirrel 
##                         1                         1                         1 
##                Guinea pig                     Horse                    Jaguar 
##                         1                         1                         1 
##                  Kangaroo Lesser short-tailed shrew          Little brown bat 
##                         1                         1                         1 
##                       Man                  Mole rat           Mountain beaver 
##                         1                         1                         1 
##                     Mouse                Musk shrew       N. American opossum 
##                         1                         1                         1 
##     Nine-banded armadillo                     Okapi                Owl monkey 
##                         1                         1                         1 
##              Patas monkey                Phanlanger                       Pig 
##                         1                         1                         1 
##                    Rabbit                   Raccoon                       Rat 
##                         1                         1                         1 
##                   Red fox             Rhesus monkey    Rock hyrax (Hetero. b) 
##                         1                         1                         1 
## Rock hyrax (Procavia hab)                  Roe deer                     Sheep 
##                         1                         1                         1 
##                Slow loris           Star nosed mole                    Tenrec 
##                         1                         1                         1 
##                Tree hyrax                Tree shrew                    Vervet 
##                         1                         1                         1 
##             Water opossum     Yellow-bellied marmot 
##                         1                         1
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
small_mammals<-filter(msleep, bodywt<=1)
small_mammals
```

```
## # A tibble: 36 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  2 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  3 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  4 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055   0.728
##  5 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064   0.42 
##  6 Star… Cond… omni  Sori… lc         10.3     2.2  NA      13.7  0.001    0.06 
##  7 Afri… Cric… omni  Rode… <NA>        8.3     2    NA      15.7  0.0066   1    
##  8 Less… Cryp… omni  Sori… lc          9.1     1.4   0.15   14.9  0.00014  0.005
##  9 Big … Epte… inse… Chir… lc         19.7     3.9   0.117   4.3  0.0003   0.023
## 10 Euro… Erin… omni  Erin… lc         10.1     3.5   0.283  13.9  0.0035   0.77 
## # … with 26 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

```r
large_mammals<-filter(msleep,bodywt <=200) 
large_mammals
```

```
## # A tibble: 76 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Chee… Acin… carni Carn… lc         12.1    NA    NA      11.9 NA       50    
##  2 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  3 Moun… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA        1.35 
##  4 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  5 Thre… Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA        3.85 
##  6 Nort… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA       20.5  
##  7 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  8 Dog   Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07    14    
##  9 Roe … Capr… herbi Arti… lc          3      NA    NA      21    0.0982  14.8  
## 10 Goat  Capri herbi Arti… lc          5.3     0.6  NA      18.7  0.115   33.5  
## # … with 66 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

8. What is the mean weight for both the small and large mammals?

```r
w <- small_mammals$bodywt
mean(w)
```

```
## [1] 0.2596667
```

```r
w <- large_mammals$bodywt
mean(w)
```

```
## [1] 20.52396
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
w <- large_mammals$sleep_total
mean(w)
```

```
## [1] 11.09079
```


```r
w <- small_mammals$sleep_total
mean(w)
```

```
## [1] 12.65833
```
The smaller mammals sleep longer than average

10. Which animal is the sleepiest among the entire dataframe?

```r
max(msleep$sleep_total)
```

```
## [1] 19.9
```

Writing Data to File

```r
write.csv(sleep, "mammals_sleep_allison_cicchetti_1976.csv", row.names = FALSE)
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
