---
title: "Midterm 1"
author: "Maggie Bauer"
date: "2022-01-27"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   2.1.1     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library("janitor")
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  
We have practiced how to  put data into a form that is concise and provides the necessary information. Functions like group_by allow for the data to be put in a form that better suits the question. There are also functions like tabyl which allow the data to be put in a format that is easily readable. I have also practiced how to analyze data using functons like mean and median and to put that into a table using the mutate function. 
2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  
I think the most helpful thing I have learned so far is how to take a huge amount of data and be able to interpret it using functions. As someone who wants to work in a lab in the future that is something that is important for me to learn. I have also become more familiar with R and Github and how they work together. I think I need more work when it comes to taking out NAs and changing classes of data. Also sometimes I get stuck with an error and I don't really understand how to fix it. I want to be better at understanding what it means and how to fix it. 
In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.

```r
elephants <- readr::read_csv(file = "data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
```

```
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
glimpse(elephants)
```

```
## Rows: 288
## Columns: 3
## $ Age    <dbl> 1.40, 17.50, 12.75, 11.17, 12.67, 12.67, 12.25, 12.17, 28.17, 1…
## $ Height <dbl> 120.00, 227.00, 235.00, 210.00, 220.00, 189.00, 225.00, 204.00,…
## $ Sex    <chr> "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M"…
```

```r
names(elephants)
```

```
## [1] "Age"    "Height" "Sex"
```

```r
class("Age")
```

```
## [1] "character"
```

```r
class("Height")
```

```
## [1] "character"
```

```r
class("Sex")
```

```
## [1] "character"
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.

```r
elephants <- select_all(elephants, tolower)
```

```r
names(elephants)
```

```
## [1] "age"    "height" "sex"
```

```r
sex <- as.factor("sex")
class(sex)
```

```
## [1] "factor"
```

5. (2 points) How many male and female elephants are represented in the data?

```r
elephants %>% 
  group_by(sex) %>% 
  summarize(n=n())
```

```
## # A tibble: 2 × 2
##   sex       n
##   <chr> <int>
## 1 F       150
## 2 M       138
```

6. (2 points) What is the average age all elephants in the data?

```r
mean(elephants$age)
```

```
## [1] 10.97132
```


7. (2 points) How does the average age and height of elephants compare by sex?

```r
female_elephants <- filter(elephants, sex == "F")
female_elephants
```

```
## # A tibble: 150 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1 11.1   218.  F    
##  2  2.33  133.  F    
##  3  2.42  145.  F    
##  4 26.5   206.  F    
##  5 11.8   207   F    
##  6  0.33   85.6 F    
##  7 26.8   227.  F    
##  8 13.4   203   F    
##  9 28.4   228.  F    
## 10  2.08  131.  F    
## # … with 140 more rows
```

```r
mean(female_elephants$age)
```

```
## [1] 12.8354
```

```r
mean(female_elephants$height)
```

```
## [1] 190.0307
```

```r
male_elephants <- filter(elephants, sex == "M")
male_elephants
```

```
## # A tibble: 138 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 128 more rows
```

```r
mean(male_elephants$age)
```

```
## [1] 8.945145
```

```r
mean(male_elephants$height)
```

```
## [1] 185.1312
```
Females have a higher average age and height.  
8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

```r
female_elephants20 <- filter(female_elephants, age > 20) 
female_elephants20
```

```
## # A tibble: 37 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1  26.5   206. F    
##  2  26.8   227. F    
##  3  28.4   228. F    
##  4  27.2   226. F    
##  5  25.4   240. F    
##  6  23.3   238. F    
##  7  26.8   235. F    
##  8  27.8   265  F    
##  9  28.2   216. F    
## 10  26.1   216. F    
## # … with 27 more rows
```

```r
mean(female_elephants20$height)
```

```
## [1] 232.2014
```

```r
min(female_elephants20$height)
```

```
## [1] 192.54
```

```r
max(female_elephants20$height)
```

```
## [1] 277.8
```

```r
female_elephants20 %>% 
  summarize(n=n())
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1    37
```

```r
male_elephants20 <- filter(male_elephants, age > 20) 
male_elephants20
```

```
## # A tibble: 13 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1  28.2   266. M    
##  2  25.4   252. M    
##  3  26.5   258. M    
##  4  26.7   269. M    
##  5  25.7   237. M    
##  6  28.8   302. M    
##  7  24.2   253. M    
##  8  23.9   282. M    
##  9  26.1   304. M    
## 10  25.4   294. M    
## 11  24.2   287. M    
## 12  21.2   273. M    
## 13  21.3   229. M
```

```r
mean(male_elephants20$height)
```

```
## [1] 269.5931
```

```r
min(male_elephants20$height)
```

```
## [1] 228.69
```

```r
max(male_elephants20$height)
```

```
## [1] 304.06
```

```r
male_elephants20 %>% 
  summarize(n=n())
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1    13
```

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
transect <- readr::read_csv(file = "data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
```

```
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
glimpse(transect)
```

```
## Rows: 24
## Columns: 26
## $ TransectID              <dbl> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16, …
## $ Distance                <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.06…
## $ HuntCat                 <chr> "Moderate", "None", "None", "None", "None", "N…
## $ NumHouseholds           <dbl> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 56…
## $ LandUse                 <chr> "Park", "Park", "Park", "Logging", "Park", "Pa…
## $ Veg_Rich                <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.7…
## $ Veg_Stems               <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.2…
## $ Veg_liana               <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, 8…
## $ Veg_DBH                 <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.2…
## $ Veg_Canopy              <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.00…
## $ Veg_Understory          <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.71…
## $ RA_Apes                 <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.1…
## $ RA_Birds                <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.6…
## $ RA_Elephant             <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.43…
## $ RA_Monkeys              <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.2…
## $ RA_Rodent               <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.26…
## $ RA_Ungulate             <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, 8…
## $ Rich_AllSpecies         <dbl> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 22…
## $ Evenness_AllSpecies     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.81…
## $ Diversity_AllSpecies    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.56…
## $ Rich_BirdSpecies        <dbl> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, 1…
## $ Evenness_BirdSpecies    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.80…
## $ Diversity_BirdSpecies   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.92…
## $ Rich_MammalSpecies      <dbl> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11, …
## $ Evenness_MammalSpecies  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.77…
## $ Diversity_MammalSpecies <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.92…
```

```r
HuntCat <- as.factor("HuntCat")
class(HuntCat)
```

```
## [1] "factor"
```

```r
LandUse <- as.factor("LandUse")
class(LandUse)
```

```
## [1] "factor"
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?

```r
transect_2 <- filter(transect, HuntCat == "High" | HuntCat == "Moderate" )
transect_2
```

```
## # A tibble: 15 × 26
##    TransectID Distance HuntCat  NumHouseholds LandUse Veg_Rich Veg_Stems
##         <dbl>    <dbl> <chr>            <dbl> <chr>      <dbl>     <dbl>
##  1          1     7.14 Moderate            54 Park        16.7      31.2
##  2          8     5.78 High                25 Neither     12.6      23.7
##  3          9     5.13 High                73 Logging     16        27.1
##  4         13     6.61 Moderate            46 Logging     12.4      23.4
##  5         14     8.23 Moderate            56 Logging     15.8      30.2
##  6         15     2.7  High                46 Neither     10.9      25.4
##  7         16     6.1  Moderate            36 Logging     14.6      39.1
##  8         17     3.83 High                19 Neither     14.2      32.6
##  9         19    14.0  Moderate            54 Logging     14.9      35  
## 10         20     6.61 Moderate            24 Logging     13.2      26.9
## 11         21     5.14 High                24 Neither     16.2      34.9
## 12         22     5.33 High                13 Logging     17.1      41.6
## 13         25    15.0  Moderate            54 Logging     15        26.8
## 14         26    11.2  Moderate            73 Logging     18.8      39.1
## 15         27     2.92 High                13 Logging     12.4      47.6
## # … with 19 more variables: Veg_liana <dbl>, Veg_DBH <dbl>, Veg_Canopy <dbl>,
## #   Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>, RA_Elephant <dbl>,
## #   RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, …
```

```r
mean(transect_2$Diversity_BirdSpecies)
```

```
## [1] 1.639733
```

```r
mean(transect_2$Diversity_MammalSpecies)
```

```
## [1] 1.7086
```
Higher mammal diversity 
11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  


```r
 transect %>% 
  filter(Distance < 3) %>% 
  summarise(across(c(RA_Apes, RA_Birds, RA_Elephant, RA_Monkeys, RA_Rodent, RA_Ungulate), mean))
```

```
## # A tibble: 1 × 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0.12     76.6       0.145       17.3      3.90        1.87
```


```r
transect %>% 
  filter(Distance > 25) %>% 
  summarize(across(c(RA_Apes, RA_Birds, RA_Elephant, RA_Monkeys, RA_Rodent, RA_Ungulate), mean))
```

```
## # A tibble: 1 × 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`

```r
transect %>% 
  group_by(LandUse) %>% 
  mutate(mean_diveristy= mean(Diversity_AllSpecies)) %>% 
  arrange(mean_diveristy)
```

```
## # A tibble: 24 × 27
## # Groups:   LandUse [3]
##    TransectID Distance HuntCat  NumHouseholds LandUse Veg_Rich Veg_Stems
##         <dbl>    <dbl> <chr>            <dbl> <chr>      <dbl>     <dbl>
##  1          3    20.8  None                29 Logging     12.4      29.4
##  2          7    19.8  None                54 Logging     13.2      32.6
##  3          9     5.13 High                73 Logging     16        27.1
##  4         13     6.61 Moderate            46 Logging     12.4      23.4
##  5         14     8.23 Moderate            56 Logging     15.8      30.2
##  6         16     6.1  Moderate            36 Logging     14.6      39.1
##  7         18    18.8  None                17 Logging     11.8      37  
##  8         19    14.0  Moderate            54 Logging     14.9      35  
##  9         20     6.61 Moderate            24 Logging     13.2      26.9
## 10         22     5.33 High                13 Logging     17.1      41.6
## # … with 14 more rows, and 20 more variables: Veg_liana <dbl>, Veg_DBH <dbl>,
## #   Veg_Canopy <dbl>, Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>,
## #   RA_Elephant <dbl>, RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, …
```


```r
getwd()
```

```
## [1] "/Users/maggiebauer/Downloads/Untitled/BIS15W2022_mbauer/midterm1"
```

