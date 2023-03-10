---
title: "BIS 15L Midterm 2"
author: "Grace ochieng"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. To receive full credit, all plots must have clearly labeled axes, a title, and consistent aesthetics. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library("tidyverse")
library("janitor")
library("naniar")
```

## Data
These data are from a study on surgical residents. The study was originally published by Sessier et al. “Operation Timing and 30-Day Mortality After Elective General Surgery”. Anesth Analg 2011; 113: 1423-8. The data were cleaned for instructional use by Amy S. Nowacki, “Surgery Timing Dataset”, TSHS Resources Portal (2016). Available at https://www.causeweb.org/tshs/surgery-timing/.

Descriptions of the variables and the study are included as pdf's in the data folder.  

Please run the following chunk to import the data.

```r
surgery <- read_csv("data/surgery.csv")
```

1. (2 points) Use the summary function(s) of your choice to explore the data and get an idea of its structure. Please also check for NA's.

```r
summary(surgery)
```

```
##    ahrq_ccs              age           gender              race          
##  Length:32001       Min.   : 1.00   Length:32001       Length:32001      
##  Class :character   1st Qu.:48.20   Class :character   Class :character  
##  Mode  :character   Median :58.60   Mode  :character   Mode  :character  
##                     Mean   :57.66                                        
##                     3rd Qu.:68.30                                        
##                     Max.   :90.00                                        
##                     NA's   :2                                            
##   asa_status             bmi        baseline_cancer    baseline_cvd      
##  Length:32001       Min.   : 2.15   Length:32001       Length:32001      
##  Class :character   1st Qu.:24.60   Class :character   Class :character  
##  Mode  :character   Median :28.19   Mode  :character   Mode  :character  
##                     Mean   :29.45                                        
##                     3rd Qu.:32.81                                        
##                     Max.   :92.59                                        
##                     NA's   :3290                                         
##  baseline_dementia  baseline_diabetes  baseline_digestive baseline_osteoart 
##  Length:32001       Length:32001       Length:32001       Length:32001      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  baseline_psych     baseline_pulmonary baseline_charlson mortality_rsi    
##  Length:32001       Length:32001       Min.   : 0.000    Min.   :-4.4000  
##  Class :character   Class :character   1st Qu.: 0.000    1st Qu.:-1.2400  
##  Mode  :character   Mode  :character   Median : 0.000    Median :-0.3000  
##                                        Mean   : 1.184    Mean   :-0.5316  
##                                        3rd Qu.: 2.000    3rd Qu.: 0.0000  
##                                        Max.   :13.000    Max.   : 4.8600  
##                                                                           
##  complication_rsi  ccsmort30rate      ccscomplicationrate      hour      
##  Min.   :-4.7200   Min.   :0.000000   Min.   :0.01612     Min.   : 6.00  
##  1st Qu.:-0.8400   1st Qu.:0.000789   1st Qu.:0.08198     1st Qu.: 7.65  
##  Median :-0.2700   Median :0.002764   Median :0.10937     Median : 9.65  
##  Mean   :-0.4091   Mean   :0.004312   Mean   :0.13325     Mean   :10.38  
##  3rd Qu.: 0.0000   3rd Qu.:0.007398   3rd Qu.:0.18337     3rd Qu.:12.72  
##  Max.   :13.3000   Max.   :0.016673   Max.   :0.46613     Max.   :19.00  
##                                                                          
##      dow               month            moonphase            mort30         
##  Length:32001       Length:32001       Length:32001       Length:32001      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  complication      
##  Length:32001      
##  Class :character  
##  Mode  :character  
##                    
##                    
##                    
## 
```

```r
naniar::miss_var_summary(surgery)
```

```
## # A tibble: 25 × 3
##    variable          n_miss pct_miss
##    <chr>              <int>    <dbl>
##  1 bmi                 3290 10.3    
##  2 race                 480  1.50   
##  3 asa_status             8  0.0250 
##  4 gender                 3  0.00937
##  5 age                    2  0.00625
##  6 ahrq_ccs               0  0      
##  7 baseline_cancer        0  0      
##  8 baseline_cvd           0  0      
##  9 baseline_dementia      0  0      
## 10 baseline_diabetes      0  0      
## # … with 15 more rows
```

```r
names(surgery)
```

```
##  [1] "ahrq_ccs"            "age"                 "gender"             
##  [4] "race"                "asa_status"          "bmi"                
##  [7] "baseline_cancer"     "baseline_cvd"        "baseline_dementia"  
## [10] "baseline_diabetes"   "baseline_digestive"  "baseline_osteoart"  
## [13] "baseline_psych"      "baseline_pulmonary"  "baseline_charlson"  
## [16] "mortality_rsi"       "complication_rsi"    "ccsmort30rate"      
## [19] "ccscomplicationrate" "hour"                "dow"                
## [22] "month"               "moonphase"           "mort30"             
## [25] "complication"
```

2. (3 points) Let's explore the participants in the study. Show a count of participants by race AND make a plot that visually represents your output.

```r
participants <-surgery %>%
  filter(race!="Other", race!="NA") %>% 
  count(race) %>%
  arrange(desc(n)) 
```


```r
participants %>% 
  ggplot(aes(x=race, y=n))+
  geom_col()
```

![](midterm_2_files/figure-html/unnamed-chunk-7-1.png)<!-- -->


3. (2 points) What is the mean age of participants by gender? (hint: please provide a number for each) Since only three participants do not have gender indicated, remove these participants from the data.

```r
age_surgery<-
  na.omit(surgery) %>% 
  group_by(gender)
surgery
```

```
## # A tibble: 32,001 × 25
##    ahrq_ccs   age gender race      asa_s…¹   bmi basel…² basel…³ basel…⁴ basel…⁵
##    <chr>    <dbl> <chr>  <chr>     <chr>   <dbl> <chr>   <chr>   <chr>   <chr>  
##  1 <Other>   67.8 M      Caucasian I-II     28.0 No      Yes     No      No     
##  2 <Other>   39.5 F      Caucasian I-II     37.8 No      Yes     No      No     
##  3 <Other>   56.5 F      Caucasian I-II     19.6 No      No      No      No     
##  4 <Other>   71   M      Caucasian III      32.2 No      Yes     No      No     
##  5 <Other>   56.3 M      African … I-II     24.3 Yes     No      No      No     
##  6 <Other>   57.7 F      Caucasian I-II     40.3 No      Yes     No      No     
##  7 <Other>   56.6 M      Other     IV-VI    64.6 No      Yes     No      Yes    
##  8 <Other>   64.2 F      Caucasian III      43.2 No      Yes     No      No     
##  9 <Other>   66.2 M      Caucasian III      28.0 No      Yes     No      No     
## 10 <Other>   20.1 F      Caucasian I-II     27.4 Yes     No      No      No     
## # … with 31,991 more rows, 15 more variables: baseline_digestive <chr>,
## #   baseline_osteoart <chr>, baseline_psych <chr>, baseline_pulmonary <chr>,
## #   baseline_charlson <dbl>, mortality_rsi <dbl>, complication_rsi <dbl>,
## #   ccsmort30rate <dbl>, ccscomplicationrate <dbl>, hour <dbl>, dow <chr>,
## #   month <chr>, moonphase <chr>, mort30 <chr>, complication <chr>, and
## #   abbreviated variable names ¹​asa_status, ²​baseline_cancer, ³​baseline_cvd,
## #   ⁴​baseline_dementia, ⁵​baseline_diabetes
```

4. (SIPPED)(3 points) Make a plot that shows the range of age associated with gender.

```r
#age_surgery %>% 
#  ggplot(aes(x=gender, y=avg_age))+
#  geom_col()
```


5. (Check) (2 points) How healthy are the participants? The variable `asa_status` is an evaluation of patient physical status prior to surgery. Lower numbers indicate fewer comorbidities (presence of two or more diseases or medical conditions in a patient). Make a plot that compares the number of `asa_status` I-II, I-II, and IV-V.

```r
asa_surgery<-surgery %>% 
  group_by(asa_status) %>% 
    count(asa_status) 
```

```r
asa_surgery %>% 
  ggplot(aes(x=asa_status, y=n))+
  geom_col()
```

![](midterm_2_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

6. (3 points) Create a plot that displays the distribution of body mass index for each `asa_status` as a probability distribution- not a histogram. (hint: use faceting!)

```r
surgery %>% 
  ggplot(aes(x=bmi))+
  geom_density()+
  facet_wrap(~asa_status)
```

```
## Warning: Removed 3290 rows containing non-finite values (`stat_density()`).
```

![](midterm_2_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

The variable `ccsmort30rate` is a measure of the overall 30-day mortality rate associated with each type of operation. The variable `ccscomplicationrate` is a measure of the 30-day in-hospital complication rate. The variable `ahrq_ccs` lists each type of operation.  

7. (4 points) What are the 5 procedures associated with highest risk of 30-day mortality AND how do they compare with the 5 procedures with highest risk of complication? (hint: no need for a plot here)

```r
surgery %>% 
  group_by(ahrq_ccs) %>% 
  count(ccscomplicationrate) %>%
  arrange(desc(ccscomplicationrate)) 
```

```
## # A tibble: 23 × 3
## # Groups:   ahrq_ccs [23]
##    ahrq_ccs                                  ccscomplicationrate     n
##    <chr>                                                   <dbl> <int>
##  1 Small bowel resection                                   0.466   620
##  2 Colorectal resection                                    0.312  2519
##  3 Nephrectomy; partial or complete                        0.197  2894
##  4 Gastrectomy; partial and total                          0.190   394
##  5 Spinal fusion                                           0.183  2694
##  6 Hysterectomy; abdominal and vaginal                     0.151  2548
##  7 Other hernia repair                                     0.143  1242
##  8 Oophorectomy; unilateral and bilateral                  0.135   576
##  9 Open prostatectomy                                      0.109  2679
## 10 Laminectomy; excision intervertebral disc               0.106  2535
## # … with 13 more rows
```


```r
surgery %>% 
  group_by(ahrq_ccs) %>% 
  count(ccsmort30rate) %>%
  arrange(desc(ccsmort30rate)) 
```

```
## # A tibble: 23 × 3
## # Groups:   ahrq_ccs [23]
##    ahrq_ccs                                             ccsmort30rate     n
##    <chr>                                                        <dbl> <int>
##  1 Colorectal resection                                       0.0167   2519
##  2 Small bowel resection                                      0.0129    620
##  3 Gastrectomy; partial and total                             0.0127    394
##  4 Endoscopy and endoscopic biopsy of the urinary tract       0.00811   370
##  5 Spinal fusion                                              0.00742  2694
##  6 Hip replacement; total and partial                         0.00740  2298
##  7 Genitourinary incontinence procedures                      0.00433   462
##  8 <Other>                                                    0.00425   941
##  9 Other hernia repair                                        0.00403  1242
## 10 Arthroplasty knee                                          0.00296  3379
## # … with 13 more rows
```
8. (3 points) Make a plot that compares the `ccsmort30rate` for all listed `ahrq_ccs` procedures.

```r
p <- surgery %>% 
  ggplot(aes(x=ccsmort30rate, y=ahrq_ccs))+
  geom_col()
p
```

![](midterm_2_files/figure-html/unnamed-chunk-15-1.png)<!-- -->


9.(CHECK) (4 points) When is the best month to have surgery? Make a chart that shows the 30-day mortality and complications for the patients by month. `mort30` is the variable that shows whether or not a patient survived 30 days post-operation.

```r
surgery %>% 
  group_by(month) %>% 
  mutate(months_surgery=if_else(mort30=="Yes",1,0)) %>% 
  summarise(sum=sum(months_surgery))
```

```
## # A tibble: 12 × 2
##    month   sum
##    <chr> <dbl>
##  1 Apr      12
##  2 Aug       9
##  3 Dec       4
##  4 Feb      17
##  5 Jan      19
##  6 Jul      12
##  7 Jun      14
##  8 Mar      12
##  9 May      10
## 10 Nov       5
## 11 Oct       8
## 12 Sep      16
```

```r
m<-surgery %>% 
  group_by(month) %>% 
  mutate(months_surgery=if_else(mort30=="Yes",1,0)) %>% 
  summarise(sum=sum(months_surgery))
```

10. (4 points) Make a plot that visualizes the chart from question #9. Make sure that the months are on the x-axis. Do a search online and figure out how to order the months Jan-Dec.

```r
m %>% 
  ggplot(aes(x=month, y=sum))+
  geom_col()
```

![](midterm_2_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

```r
m
```

```
## # A tibble: 12 × 2
##    month   sum
##    <chr> <dbl>
##  1 Apr      12
##  2 Aug       9
##  3 Dec       4
##  4 Feb      17
##  5 Jan      19
##  6 Jul      12
##  7 Jun      14
##  8 Mar      12
##  9 May      10
## 10 Nov       5
## 11 Oct       8
## 12 Sep      16
```

```r
# January
```


Please provide the names of the students you have worked with with during the exam:

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
