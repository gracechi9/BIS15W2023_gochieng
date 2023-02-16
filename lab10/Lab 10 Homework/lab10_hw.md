---
title: "Lab 10 Homework"
author: "Grace Ochieng"
date: "02:14:2023"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```


```r
options(scipen=999)
```

## Desert Ecology
For this assignment, we are going to use a modified data set on [desert ecology](http://esapubs.org/archive/ecol/E090/118/). The data are from: S. K. Morgan Ernest, Thomas J. Valone, and James H. Brown. 2009. Long-term monitoring and experimental manipulation of a Chihuahuan Desert ecosystem near Portal, Arizona, USA. Ecology 90:1708.

```r
deserts <- read_csv(here("lab10", "data", "surveys_complete.csv"), na = c("NA"))
```

```
## Rows: 34786 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (6): species_id, sex, genus, species, taxa, plot_type
## dbl (7): record_id, month, day, year, plot_id, hindfoot_length, weight
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Use the function(s) of your choice to get an idea of its structure, including how NA's are treated. Are the data tidy?  

```r
glimpse(deserts)
```

```
## Rows: 34,786
## Columns: 13
## $ record_id       <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,…
## $ month           <dbl> 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, …
## $ day             <dbl> 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16…
## $ year            <dbl> 1977, 1977, 1977, 1977, 1977, 1977, 1977, 1977, 1977, …
## $ plot_id         <dbl> 2, 3, 2, 7, 3, 1, 2, 1, 1, 6, 5, 7, 3, 8, 6, 4, 3, 2, …
## $ species_id      <chr> "NL", "NL", "DM", "DM", "DM", "PF", "PE", "DM", "DM", …
## $ sex             <chr> "M", "M", "F", "M", "M", "M", "F", "M", "F", "F", "F",…
## $ hindfoot_length <dbl> 32, 33, 37, 36, 35, 14, NA, 37, 34, 20, 53, 38, 35, NA…
## $ weight          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ genus           <chr> "Neotoma", "Neotoma", "Dipodomys", "Dipodomys", "Dipod…
## $ species         <chr> "albigula", "albigula", "merriami", "merriami", "merri…
## $ taxa            <chr> "Rodent", "Rodent", "Rodent", "Rodent", "Rodent", "Rod…
## $ plot_type       <chr> "Control", "Long-term Krat Exclosure", "Control", "Rod…
```


```r
naniar::miss_var_summary(deserts)
```

```
## # A tibble: 13 × 3
##    variable        n_miss pct_miss
##    <chr>            <int>    <dbl>
##  1 hindfoot_length   3348     9.62
##  2 weight            2503     7.20
##  3 record_id            0     0   
##  4 month                0     0   
##  5 day                  0     0   
##  6 year                 0     0   
##  7 plot_id              0     0   
##  8 species_id           0     0   
##  9 sex                  0     0   
## 10 genus                0     0   
## 11 species              0     0   
## 12 taxa                 0     0   
## 13 plot_type            0     0
```

```r
deserts
```

```
## # A tibble: 34,786 × 13
##    record…¹ month   day  year plot_id speci…² sex   hindf…³ weight genus species
##       <dbl> <dbl> <dbl> <dbl>   <dbl> <chr>   <chr>   <dbl>  <dbl> <chr> <chr>  
##  1        1     7    16  1977       2 NL      M          32     NA Neot… albigu…
##  2        2     7    16  1977       3 NL      M          33     NA Neot… albigu…
##  3        3     7    16  1977       2 DM      F          37     NA Dipo… merria…
##  4        4     7    16  1977       7 DM      M          36     NA Dipo… merria…
##  5        5     7    16  1977       3 DM      M          35     NA Dipo… merria…
##  6        6     7    16  1977       1 PF      M          14     NA Pero… flavus 
##  7        7     7    16  1977       2 PE      F          NA     NA Pero… eremic…
##  8        8     7    16  1977       1 DM      M          37     NA Dipo… merria…
##  9        9     7    16  1977       1 DM      F          34     NA Dipo… merria…
## 10       10     7    16  1977       6 PF      F          20     NA Pero… flavus 
## # … with 34,776 more rows, 2 more variables: taxa <chr>, plot_type <chr>, and
## #   abbreviated variable names ¹​record_id, ²​species_id, ³​hindfoot_length
```

```r
# Our data is tidy ,each variable has its own column, each observation has its own row and each value has its own cell
```

2. How many genera and species are represented in the data? What are the total number of observations? Which species is most/ least frequently sampled in the study?

```r
deserts %>% 
  count(genus,species) %>%
  arrange(desc(n)) 
```

```
## # A tibble: 48 × 3
##    genus           species          n
##    <chr>           <chr>        <int>
##  1 Dipodomys       merriami     10596
##  2 Chaetodipus     penicillatus  3123
##  3 Dipodomys       ordii         3027
##  4 Chaetodipus     baileyi       2891
##  5 Reithrodontomys megalotis     2609
##  6 Dipodomys       spectabilis   2504
##  7 Onychomys       torridus      2249
##  8 Perognathus     flavus        1597
##  9 Peromyscus      eremicus      1299
## 10 Neotoma         albigula      1252
## # … with 38 more rows
```


```r
deserts %>% 
  select(species) %>% 
  summarize(total=n())
```

```
## # A tibble: 1 × 1
##   total
##   <int>
## 1 34786
```

```r
deserts %>%
  count(species, sort=T) %>% 
  top_n(1,n)
```

```
## # A tibble: 1 × 2
##   species      n
##   <chr>    <int>
## 1 merriami 10596
```

```r
# Merriami is the most frequently sampled species 
```


```r
deserts %>%
  tabyl(species) %>%
  arrange(desc(n))
```

```
##          species     n       percent
##         merriami 10596 0.30460530098
##     penicillatus  3123 0.08977749669
##            ordii  3027 0.08701776577
##          baileyi  2891 0.08310814696
##        megalotis  2609 0.07500143736
##      spectabilis  2504 0.07198298166
##         torridus  2249 0.06465244639
##           flavus  1597 0.04590927385
##         eremicus  1299 0.03734260910
##         albigula  1252 0.03599149083
##      leucogaster  1006 0.02891968033
##      maniculatus   899 0.02584373024
##          harrisi   437 0.01256252515
##        bilineata   303 0.00871040074
##        spilosoma   248 0.00712930489
##         hispidus   179 0.00514574829
##              sp.    86 0.00247225895
##        audubonii    75 0.00215603979
##       fulvescens    75 0.00215603979
##  brunneicapillus    50 0.00143735986
##          taylori    46 0.00132237107
##      fulviventer    43 0.00123612948
##     ochrognathus    43 0.00123612948
##        chlorurus    39 0.00112114069
##         leucopus    36 0.00103489910
##         squamata    16 0.00045995515
##      melanocorys    13 0.00037371356
##      intermedius     9 0.00025872477
##        gramineus     8 0.00022997758
##         montanus     8 0.00022997758
##           fuscus     5 0.00014373599
##        undulatus     5 0.00014373599
##       leucophrys     2 0.00005749439
##       savannarum     2 0.00005749439
##           clarki     1 0.00002874720
##       scutalatus     1 0.00002874720
##     tereticaudus     1 0.00002874720
##           tigris     1 0.00002874720
##        uniparens     1 0.00002874720
##          viridis     1 0.00002874720
```

```r
# for the least sampleled species we have Virdis, Uniparens, Tigris, Tereticaudus, Scutalatus and Clarki
```

3. What is the proportion of taxa included in this study? Show a table and plot that reflects this count.

```r
deserts %>% 
  count(taxa) %>%
  arrange(desc(n))
```

```
## # A tibble: 4 × 2
##   taxa        n
##   <chr>   <int>
## 1 Rodent  34247
## 2 Bird      450
## 3 Rabbit     75
## 4 Reptile    14
```



```r
deserts %>% 
  ggplot (aes(x=taxa))+
  geom_bar()+
  scale_y_log10()
```

![](lab10_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

4. For the taxa included in the study, use the fill option to show the proportion of individuals sampled by `plot_type.`

```r
deserts %>% 
  ggplot(aes(x=taxa, fill=plot_type))+
  geom_bar()+
  scale_y_log10()+
  labs(title = "Propotions Sampled of Individuals",
       x = "Taxa Group",
       y = "Count(log10)")
```

![](lab10_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


5. What is the range of weight for each species included in the study? Remove any observations of weight that are NA so they do not show up in the plot.

```r
deserts %>% 
  filter(weight!="NA") %>% 
  ggplot(aes(x=species, y=weight, fill=species))+ geom_boxplot()+
  coord_flip()+
  labs(title = "Range of Weight by Species")
```

![](lab10_hw_files/figure-html/unnamed-chunk-14-1.png)<!-- -->
6. Add another layer to your answer from #4 using `geom_point` to get an idea of how many measurements were taken for each species.


```r
deserts %>%
  ggplot(aes(x=reorder(species, weight), y= weight, fill=species))+
  geom_boxplot()+
  geom_point(size = 0.4)+
  scale_y_log10()+
  coord_flip()+
  labs(titles = "Range of Weight by Species",
       x = "Species",
       y = "Weight (log10)",
       fill = "species")
```

```
## Warning: Removed 2503 rows containing non-finite values (`stat_boxplot()`).
```

```
## Warning: Removed 2503 rows containing missing values (`geom_point()`).
```

![](lab10_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

7. [Dipodomys merriami](https://en.wikipedia.org/wiki/Merriam's_kangaroo_rat) is the most frequently sampled animal in the study. How have the number of observations of this species changed over the years included in the study?


```r
deserts %>%
  filter(species=="merriami" & genus=="Dipodomys") %>%
  ggplot(aes(x = year,color=species)) +
  labs(title = "Number of observations of Merriami over the years",
       x = "Year",
       y = "Observations")+
  geom_bar()+
  theme(plot.title = element_text(size = rel(0.95), hjust = 0.5))
```

![](lab10_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

8. What is the relationship between `weight` and `hindfoot` length? Consider whether or not over plotting is an issue.


```r
names(deserts)
```

```
##  [1] "record_id"       "month"           "day"             "year"           
##  [5] "plot_id"         "species_id"      "sex"             "hindfoot_length"
##  [9] "weight"          "genus"           "species"         "taxa"           
## [13] "plot_type"
```


```r
deserts %>% 
  ggplot(aes(x=weight, y=hindfoot_length))+
  geom_point(size=0.25, na.rm = T)+
  geom_smooth(method=lm, se=F)
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

```
## Warning: Removed 4048 rows containing non-finite values (`stat_smooth()`).
```

![](lab10_hw_files/figure-html/unnamed-chunk-18-1.png)<!-- -->


9. Which two species have, on average, the highest weight? Once you have identified them, make a new column that is a ratio of `weight` to `hindfoot_length`. Make a plot that shows the range of this new ratio and fill by sex.


```r
deserts %>% 
  filter((weight!="NA")) %>% 
  group_by(species) %>% 
  summarize (avg_weight = mean(weight, na.rm = T)) %>% 
  arrange (desc(avg_weight)) 
```

```
## # A tibble: 22 × 2
##    species      avg_weight
##    <chr>             <dbl>
##  1 albigula          159. 
##  2 spectabilis       120. 
##  3 spilosoma          93.5
##  4 hispidus           65.6
##  5 fulviventer        58.9
##  6 ochrognathus       55.4
##  7 ordii              48.9
##  8 merriami           43.2
##  9 baileyi            31.7
## 10 leucogaster        31.6
## # … with 12 more rows
```

```r
# On average Albigula and spectabilis have the highest average weight, respecitvely
```



```r
weight_hindfoot <- deserts %>% 
  filter(weight!="NA", hindfoot_length!="NA", sex!="NA") %>% 
  filter(species=="albigula"|species=="spectabilis") %>% 
  mutate(weight_to_hindfoot = weight/hindfoot_length) %>% 
  select(hindfoot_length, weight, species, sex, weight_to_hindfoot)
# New column created
```


```r
weight_hindfoot %>% 
  ggplot(aes(x=species, y=weight_to_hindfoot, fill = sex))+ geom_boxplot(na.rm = T)+
  labs(title = "Weight To Hindfoot Length Ratio",
       x = "Species",
       y = "Weight/Hindfoot Length")+
  theme(plot.title = element_text(size = rel(1), hjust = 0.5))
```

![](lab10_hw_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

10. Make one plot of your choice! Make sure to include at least two of the aesthetics options you have learned.

```r
names(deserts)
```

```
##  [1] "record_id"       "month"           "day"             "year"           
##  [5] "plot_id"         "species_id"      "sex"             "hindfoot_length"
##  [9] "weight"          "genus"           "species"         "taxa"           
## [13] "plot_type"
```


```r
deserts %>% 
  filter(species=="flavus") %>% 
  group_by(year, species) %>% 
  summarize(observations = n(),
            .groups = 'keep') %>% 
  ggplot(aes(x=year, y=observations, fill = species))+
  geom_col()+
  coord_flip() +
  labs(title = "Flavus Yearly Data",
       x = "Species Group",
       y = "Data collected")
```

![](lab10_hw_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

```r
# In this code i am looking at the lowest reported species "flavus" and comparing how the data of observations collected throught the years vary ~ 1996 was the highest data according to the table.
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
