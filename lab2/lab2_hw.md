---
title: "Lab 2 Homework"
author: "Grace Ochieng"
date: "2023:16:1"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?  
a vector in R is a way to organise data. For instance in a mean it identifies all values such as the decimal values and calculates a more accurate mean. In vectors we use concatenate as c and then place our values to get a more organised version of our data.
 for example;

```r
Gol<- 20.7
Di<-30.8
Locks<-10.2
```

```r
total_earnings<-c(Gol,Di,Locks)
mean(total_earnings)
```

```
## [1] 20.56667
```
 

2. What is a data matrix in R?  
a data matrix in R can be seen as data tables in ythe sence that they are a series of stacked vectors 

3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.  

```r
temperature<-c(spring_1,spring_2,spring_3,spring_4,spring_5,spring_6,spring_7,spring_8)
temperature
```

```
##  [1] 36.25 35.40 35.30 35.15 35.35 33.35 30.70 29.65 29.20 39.70 40.05 38.65
## [13] 31.85 31.40 29.30 30.20 30.65 29.75 32.90 32.50 32.80 36.80 36.45 33.15
```

```r
data_collected_matrix<- matrix(temperature, nrow = 8, byrow = T)
data_collected_matrix
```

```
##       [,1]  [,2]  [,3]
## [1,] 36.25 35.40 35.30
## [2,] 35.15 35.35 33.35
## [3,] 30.70 29.65 29.20
## [4,] 39.70 40.05 38.65
## [5,] 31.85 31.40 29.30
## [6,] 30.20 30.65 29.75
## [7,] 32.90 32.50 32.80
## [8,] 36.80 36.45 33.15
```

5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.


```r
scientists <- c("Jill", "Steve","Susan")
scientists
```

```
## [1] "Jill"  "Steve" "Susan"
```


```r
spring_names<-c("Bluebell Spring","Opal Spring","Riverside Spring","Too Hot Spring","Mystery Spring","Emerald Spring","Black Spring","Pearl Spring")
spring_names
```

```
## [1] "Bluebell Spring"  "Opal Spring"      "Riverside Spring" "Too Hot Spring"  
## [5] "Mystery Spring"   "Emerald Spring"   "Black Spring"     "Pearl Spring"
```


```r
colnames(data_collected_matrix) <- scientists
```


```r
rownames(data_collected_matrix) <- spring_names
```

The matrix created.


```r
data_collected_matrix
```

```
##                   Jill Steve Susan
## Bluebell Spring  36.25 35.40 35.30
## Opal Spring      35.15 35.35 33.35
## Riverside Spring 30.70 29.65 29.20
## Too Hot Spring   39.70 40.05 38.65
## Mystery Spring   31.85 31.40 29.30
## Emerald Spring   30.20 30.65 29.75
## Black Spring     32.90 32.50 32.80
## Pearl Spring     36.80 36.45 33.15
```

6. Calculate the mean temperature of all eight springs.

```r
total_data <- rowSums(data_collected_matrix)
total_data
```

```
##  Bluebell Spring      Opal Spring Riverside Spring   Too Hot Spring 
##           106.95           103.85            89.55           118.40 
##   Mystery Spring   Emerald Spring     Black Spring     Pearl Spring 
##            92.55            90.60            98.20           106.40
```
The calculated mean temperature

```r
springs_temperature <-c(total_data)
mean(springs_temperature)
```

```
## [1] 100.8125
```

7. Add this as a new column in the data matrix.  

```r
all_data_collected_matrix <- cbind(data_collected_matrix,total_data)
all_data_collected_matrix
```

```
##                   Jill Steve Susan total_data
## Bluebell Spring  36.25 35.40 35.30     106.95
## Opal Spring      35.15 35.35 33.35     103.85
## Riverside Spring 30.70 29.65 29.20      89.55
## Too Hot Spring   39.70 40.05 38.65     118.40
## Mystery Spring   31.85 31.40 29.30      92.55
## Emerald Spring   30.20 30.65 29.75      90.60
## Black Spring     32.90 32.50 32.80      98.20
## Pearl Spring     36.80 36.45 33.15     106.40
```

8. Show Susan's value for Opal Spring only.

```r
data_collected_matrix[2,3]
```

```
## [1] 33.35
```

9. Calculate the mean for Jill's column only.  

```r
jill <- all_data_collected_matrix[,1]
mean(jill)
```

```
## [1] 34.19375
```

10. Use the data matrix to perform one calculation or operation of your interest.
I would like to calculate the mean on all the total data the scientists collected

```r
total_data<- all_data_collected_matrix[,4]
mean(total_data)
```

```
## [1] 100.8125
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
