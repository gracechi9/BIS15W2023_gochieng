---
title: "Midterm 1"
author: "Grace Ochieng"
date: "2023:31:1"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?

```r
names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
summary(ecosphere)
```

```
##     order              family          common_name        scientific_name   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      diet           life_expectancy      habitat          urban_affiliate   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  migratory_strategy   log10_mass    mean_eggs_per_clutch
##  Length:551         Min.   :0.480   Min.   : 1.000      
##  Class :character   1st Qu.:1.365   1st Qu.: 3.000      
##  Mode  :character   Median :1.890   Median : 4.000      
##                     Mean   :2.012   Mean   : 4.527      
##                     3rd Qu.:2.685   3rd Qu.: 5.000      
##                     Max.   :4.040   Max.   :17.000      
##                                                         
##  mean_age_at_sexual_maturity population_size     winter_range_area  
##  Min.   : 0.200              Min.   :    15000   Min.   :       11  
##  1st Qu.: 1.000              1st Qu.:  1100000   1st Qu.:   819357  
##  Median : 1.000              Median :  4900000   Median :  2189639  
##  Mean   : 1.592              Mean   : 18446745   Mean   :  5051047  
##  3rd Qu.: 2.000              3rd Qu.: 18000000   3rd Qu.:  6778598  
##  Max.   :12.500              Max.   :300000000   Max.   :185968946  
##                              NA's   :273                            
##   range_in_cbc        strata          circles       feeder_bird       
##  Min.   :  0.00   Min.   :  1.00   Min.   :   2.0   Length:551        
##  1st Qu.:  2.35   1st Qu.:  3.00   1st Qu.:  46.5   Class :character  
##  Median : 30.30   Median : 11.00   Median : 184.0   Mode  :character  
##  Mean   : 38.48   Mean   : 32.43   Mean   : 558.9                     
##  3rd Qu.: 72.95   3rd Qu.: 42.00   3rd Qu.: 661.0                     
##  Max.   :100.00   Max.   :159.00   Max.   :3202.0                     
##                                                                       
##   median_trend   lower_95_percent_ci upper_95_percent_ci
##  Min.   :0.739   Min.   :0.5780      Min.   :    0.798  
##  1st Qu.:0.993   1st Qu.:0.9675      1st Qu.:    1.011  
##  Median :1.009   Median :0.9930      Median :    1.027  
##  Mean   :1.016   Mean   :0.9857      Mean   :   33.709  
##  3rd Qu.:1.030   3rd Qu.:1.0140      3rd Qu.:    1.055  
##  Max.   :1.396   Max.   :1.3080      Max.   :18000.000  
## 
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?

```r
table(ecosphere$order)
```

```
## 
##      Anseriformes       Apodiformes  Caprimulgiformes   Charadriiformes 
##                44                15                 5                81 
##     Ciconiiformes     Columbiformes     Coraciiformes      Cuculiformes 
##                29                11                 3                 3 
##     Falconiformes       Galliformes       Gaviiformes        Gruiformes 
##                31                21                 4                12 
##     Passeriformes        Piciformes  Podicipediformes Procellariiformes 
##               237                22                 6                 4 
##    Psittaciformes      Strigiformes     Trogoniformes 
##                 6                16                 1
```

Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?

```r
table(ecosphere$habitat)
```

```
## 
## Grassland     Ocean Shrubland   Various   Wetland  Woodland 
##        36        44        82        45       153       177
```

Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?

```r
ecosphere %>% 
  slice_max(winter_range_area)
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Procella… Proce… Sooty … Puffin… Vert… Long    Ocean   No      Long        2.9
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```


```r
ecosphere %>% 
  slice_min(winter_range_area)
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Passerif… Alaud… Skylark Alauda… Seed  Short   Grassl… No      Reside…    1.57
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
ducks<-filter(ecosphere, family=="Anatidae")
ducks %>% 
  select(-order,-family)
```

```
## # A tibble: 44 × 19
##    commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶ mean_…⁷ mean_…⁸
##    <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>   <dbl>
##  1 "Ameri… Anas r… Vege… Long    Wetland No      Short      3.09     9       1  
##  2 "Ameri… Anas a… Vege… Middle  Wetland No      Short      2.88     7.5     1  
##  3 "Barro… Buceph… Inve… Middle  Wetland No      Modera…    2.96    10.5     3  
##  4 "Black… Branta… Vege… Long    Wetland No      Modera…    3.11     3.5     2.5
##  5 "Black… Melani… Inve… Middle  Wetland No      Modera…    3.02     9.5     2  
##  6 "Black… Dendro… Vege… Short   Wetland No      Withdr…    2.88    13.5     1  
##  7 "Blue-… Anas d… Vege… Middle  Wetland No      Modera…    2.56    10       0.6
##  8 "Buffl… Buceph… Inve… Middle  Wetland No      Short      2.6      8.5     2  
##  9 "Cackl… Branta… Vege… Middle  Wetland Yes     Short      3.45     5       1  
## 10 "Canva… Aythya… Vege… Middle  Wetland No      Short      3.08     8       1  
## # … with 34 more rows, 9 more variables: population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass, ⁷​mean_eggs_per_clutch, ⁸​mean_age_at_sexual_maturity
```

 Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.

```r
filter(ducks,habitat!="Wetland") 
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Anserifo… Anati… Common… Somate… Inve… Middle  Ocean   No      Short      3.31
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?

```r
ducks%>% 
  select("migratory_strategy","log10_mass") %>% 
  arrange(migratory_strategy)
```

```
## # A tibble: 44 × 2
##    migratory_strategy log10_mass
##    <chr>                   <dbl>
##  1 Long                     2.89
##  2 Long                     2.85
##  3 Moderate                 2.96
##  4 Moderate                 3.11
##  5 Moderate                 3.02
##  6 Moderate                 2.56
##  7 Moderate                 3.33
##  8 Moderate                 3   
##  9 Moderate                 3.4 
## 10 Moderate                 2.75
## # … with 34 more rows
```

Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.

```r
eagle<-filter(ecosphere, family=="Accipitridae")
eagle %>% 
  select(-common_name,-scientific_name,population_size )
```

```
## # A tibble: 20 × 19
##    order    family diet  life_…¹ habitat urban…² migra…³ log10…⁴ mean_…⁵ mean_…⁶
##    <chr>    <chr>  <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>   <dbl>
##  1 Falconi… Accip… Vert… Long    Wetland No      Short      3.67     2       4.5
##  2 Falconi… Accip… Vert… Middle  Woodla… No      Long       2.66     2.5     1.5
##  3 Falconi… Accip… Vert… Middle  Woodla… Yes     Short      2.63     4.5     2  
##  4 Falconi… Accip… Vert… Middle  Grassl… No      Short      3.17     3       1.5
##  5 Falconi… Accip… Vert… Long    Various No      Short      3.63     2.5     5.5
##  6 Falconi… Accip… Vert… Middle  Woodla… No      Withdr…    2.63     2       2  
##  7 Falconi… Accip… Vert… Middle  Shrubl… Yes     Reside…    2.93     9       1  
##  8 Falconi… Accip… Inve… Middle  Woodla… No      Reside…    2.49     2.5     1  
##  9 Falconi… Accip… Vert… Middle  Woodla… No      Withdr…    2.94     3       2  
## 10 Falconi… Accip… Vert… Middle  Various No      Short      2.59     4       2.5
## 11 Falconi… Accip… Inve… Middle  Woodla… No      Short      2.78     3.5     1  
## 12 Falconi… Accip… Vert… Long    Woodla… Yes     Short      3.04     3       3  
## 13 Falconi… Accip… Vert… Middle  Grassl… No      Modera…    2.98     4.5     2.5
## 14 Falconi… Accip… Vert… Middle  Woodla… Yes     Short      2.12     4.5     2  
## 15 Falconi… Accip… Vert… Middle  Woodla… No      Withdr…    2.71     2       1.5
## 16 Falconi… Accip… Inve… Middle  Wetland No      Reside…    2.57     3       1  
## 17 Falconi… Accip… Vert… Middle  Various No      Long       2.98     3       1.5
## 18 Falconi… Accip… Vert… Middle  Grassl… No      Reside…    3.01     2.5     2  
## 19 Falconi… Accip… Vert… Short   Various No      Withdr…    2.54     4.5     1  
## 20 Falconi… Accip… Vert… Middle  Woodla… No      Short      2.88     1.5     2  
## # … with 9 more variables: population_size <dbl>, winter_range_area <dbl>,
## #   range_in_cbc <dbl>, strata <dbl>, circles <dbl>, feeder_bird <chr>,
## #   median_trend <dbl>, lower_95_percent_ci <dbl>, upper_95_percent_ci <dbl>,
## #   and abbreviated variable names ¹​life_expectancy, ²​urban_affiliate,
## #   ³​migratory_strategy, ⁴​log10_mass, ⁵​mean_eggs_per_clutch,
## #   ⁶​mean_age_at_sexual_maturity
```

Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.

```r
eagle %>%
  select(scientific_name,population_size) %>% 
  mutate(conservation_status=ifelse(population_size<250000,"threatened","safe")) %>% 
  arrange(conservation_status)
```

```
## # A tibble: 20 × 3
##    scientific_name          population_size conservation_status
##    <chr>                              <dbl> <chr>              
##  1 Buteo platypterus                1700000 safe               
##  2 Accipiter cooperii                700000 safe               
##  3 Circus cyaneus                    700000 safe               
##  4 Buteo lineatus                   1100000 safe               
##  5 Buteo jamaicensis                2000000 safe               
##  6 Buteo lagopus                     300000 safe               
##  7 Accipiter striatus                500000 safe               
##  8 Buteo swainsoni                   540000 safe               
##  9 Buteo regalis                      80000 threatened         
## 10 Aquila chrysaetos                 130000 threatened         
## 11 Parabuteo unicinctus               50000 threatened         
## 12 Accipiter gentilis                200000 threatened         
## 13 Haliaeetus leucocephalus              NA <NA>               
## 14 Buteo nitidus                         NA <NA>               
## 15 Chondrohierax uncinatus               NA <NA>               
## 16 Buteo brachyurus                      NA <NA>               
## 17 Rostrhamus sociabilis                 NA <NA>               
## 18 Buteo albicaudatus                    NA <NA>               
## 19 Elanus leucurus                       NA <NA>               
## 20 Buteo albonotatus                     NA <NA>
```

Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?

```r
anyNA(eagle,"population_size")
```

```
## [1] TRUE
```

Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.

```r
ecosphere %>% 
  filter(population_size>100000) %>% 
  group_by(family) %>% 
  select(family,population_size,habitat) %>% 
  arrange(desc(population_size))
```

```
## # A tibble: 264 × 3
## # Groups:   family [44]
##    family        population_size habitat  
##    <chr>                   <dbl> <chr>    
##  1 Turdidae            300000000 Woodland 
##  2 Emberizidae         210000000 Woodland 
##  3 Emberizidae         200000000 Woodland 
##  4 Emberizidae         170000000 Grassland
##  5 Emberizidae         140000000 Woodland 
##  6 Emberizidae         130000000 Various  
##  7 Parulidae           130000000 Woodland 
##  8 Icteridae           120000000 Various  
##  9 Icteridae           110000000 Various  
## 10 Polioptilidae       110000000 Woodland 
## # … with 254 more rows
```

```r
# In this code chunk I am trying to compare the population size and the habitat. By writing ths code chunk I can identify that Woodland habitat has most population in the ecosphere data. 
```

Please provide the names of the students you have worked with with during the exam:

```r
#Isaac Yang
```

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
