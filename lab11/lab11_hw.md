---
title: "Lab 11 Homework"
author: "Maggie Bauer"
date: "2022-02-15"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.**  

```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …
```

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**

```r
gapminder %>% 
  group_by(year) %>% 
  summarize(mean_lifeExp=mean(lifeExp)) %>% 
  ggplot(aes(x=year, y=mean_lifeExp)) + geom_point(na.rm=T) + geom_smooth(method="lm") 
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](lab11_hw_files/figure-html/unnamed-chunk-4-1.png)<!-- -->
Overall life expectancy increased 
**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**

```r
gapminder %>% 
  ggplot(aes(x=year, y=lifeExp)) +
  geom_boxplot()
```

```
## Warning: Continuous x aesthetic -- did you forget aes(group=...)?
```

![](lab11_hw_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
gapminder %>% 
  summarize(mean_lifeExp=mean(lifeExp),
            min_lifeExp=min(lifeExp),
            max_lifeExp=max(lifeExp))
```

```
## # A tibble: 1 × 3
##   mean_lifeExp min_lifeExp max_lifeExp
##          <dbl>       <dbl>       <dbl>
## 1         59.5        23.6        82.6
```
**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**

```r
gapminder %>% 
  group_by(continent) %>% 
  ggplot(aes(x=continent, y=lifeExp)) +
  geom_boxplot() + coord_flip()
```

![](lab11_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
gapminder %>% 
  group_by(continent) %>% 
  summarize(mean_lifeExp=mean(lifeExp),
            min_lifeExp=min(lifeExp),
            max_lifeExp=max(lifeExp))
```

```
## # A tibble: 5 × 4
##   continent mean_lifeExp min_lifeExp max_lifeExp
##   <fct>            <dbl>       <dbl>       <dbl>
## 1 Africa            48.9        23.6        76.4
## 2 Americas          64.7        37.6        80.7
## 3 Asia              60.1        28.8        82.6
## 4 Europe            71.9        43.6        81.8
## 5 Oceania           74.3        69.1        81.2
```

**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
gapminder %>% 
  group_by(year, continent) %>% 
  summarize(mean_lifeExp=mean(lifeExp)) %>% 
  ggplot(aes(x=year, y=mean_lifeExp, fill= continent)) + geom_point(na.rm=T) + geom_smooth(method="lm") 
```

```
## `summarise()` has grouped output by 'year'. You can override using the
## `.groups` argument.
## `geom_smooth()` using formula 'y ~ x'
```

![](lab11_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder %>% 
  ggplot(aes(x=gdpPercap, y=lifeExp)) + geom_point(na.rm=T) + geom_smooth(method="lm") 
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](lab11_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
Positive relation- yes having more morey does help you live longer 
**7. Which countries have had the largest population growth since 1952?**

```r
gapminder %>% 
  select(country, year, pop) %>% 
  filter(year == "1952" | year == "2007" ) %>% 
  pivot_wider(names_from = "year",
              names_prefix = "p",
              values_from = "pop") %>% 
  mutate(difference=p2007-p1952) %>% 
  arrange(difference)
```

```
## # A tibble: 142 × 4
##    country                 p1952   p2007 difference
##    <fct>                   <int>   <int>      <int>
##  1 Bulgaria              7274900 7322858      47958
##  2 Sao Tome and Principe   60011  199579     139568
##  3 Iceland                147962  301931     153969
##  4 Montenegro             413834  684736     270902
##  5 Equatorial Guinea      216964  551201     334237
##  6 Trinidad and Tobago    662850 1056608     393758
##  7 Djibouti                63149  496374     433225
##  8 Hungary               9504000 9956108     452108
##  9 Slovenia              1489518 2009245     519727
## 10 Reunion                257700  798094     540394
## # … with 132 more rows
```




```r
gapminder %>% 
  group_by(country) %>% 
  filter(year == "1952" | year == "2007" )
```

```
## # A tibble: 284 × 6
## # Groups:   country [142]
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       2007    43.8 31889923      975.
##  3 Albania     Europe     1952    55.2  1282697     1601.
##  4 Albania     Europe     2007    76.4  3600523     5937.
##  5 Algeria     Africa     1952    43.1  9279525     2449.
##  6 Algeria     Africa     2007    72.3 33333216     6223.
##  7 Angola      Africa     1952    30.0  4232095     3521.
##  8 Angola      Africa     2007    42.7 12420476     4797.
##  9 Argentina   Americas   1952    62.5 17876956     5911.
## 10 Argentina   Americas   2007    75.3 40301927    12779.
## # … with 274 more rows
```

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
gapminder_top <- gapminder %>% 
  filter(country == "China"| country == "India"| country == "United States"| country == "Indonesia"|country == "Brazil") %>% 
    select(country, year, pop) %>% 
  filter(year == "1952" | year == "2007" ) %>% 
  pivot_wider(names_from = "year",
              names_prefix = "p",
              values_from = "pop") %>% 
  mutate(difference=p2007-p1952) 

gapminder_top
```

```
## # A tibble: 5 × 4
##   country           p1952      p2007 difference
##   <fct>             <int>      <int>      <int>
## 1 Brazil         56602560  190010647  133408087
## 2 China         556263527 1318683096  762419569
## 3 India         372000000 1110396331  738396331
## 4 Indonesia      82052000  223547000  141495000
## 5 United States 157553000  301139947  143586947
```


```r
gapminder_top %>% 
   ggplot(aes(x=country, y=difference)) + geom_point(na.rm=T)+coord_flip()
```

![](lab11_hw_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder %>% 
  select(country, gdpPercap) %>% 
  filter(country == "China"| country == "India"| country == "United States"| country == "Indonesia"|country == "Brazil") %>% 
  mutate(mean_gdpPercap=mean(gdpPercap)) %>% 
   ggplot(aes(x=country, y=mean_gdpPercap)) + geom_point(na.rm=T)+coord_flip()
```

![](lab11_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …
```

**10. Make one plot of your choice that uses faceting!**

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
