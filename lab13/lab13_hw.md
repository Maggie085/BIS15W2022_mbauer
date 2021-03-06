---
title: "Lab 13 Homework"
author: "Maggie Bauer"
date: "2022-02-27"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Libraries

```r
if (!require("tidyverse")) install.packages('tidyverse')
```

```
## Loading required package: tidyverse
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.8
## ✓ tidyr   1.2.0     ✓ stringr 1.4.0
## ✓ readr   2.1.2     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
library(tidyverse)
library(shiny)
library(shinydashboard)
library(janitor)
```

## Data
The data for this assignment come from the [University of California Information Center](https://www.universityofcalifornia.edu/infocenter). Admissions data were collected for the years 2010-2019 for each UC campus. Admissions are broken down into three categories: applications, admits, and enrollees. The number of individuals in each category are presented by demographic.  

```r
UC_admit <- readr::read_csv("data/UC_admit.csv")
```

```
## Rows: 2160 Columns: 6
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Campus, Category, Ethnicity, Perc FR
## dbl (2): Academic_Yr, FilteredCountFR
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine if there are NA's and how they are treated.**  

```r
glimpse(UC_admit)
```

```
## Rows: 2,160
## Columns: 6
## $ Campus          <chr> "Davis", "Davis", "Davis", "Davis", "Davis", "Davis", …
## $ Academic_Yr     <dbl> 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2018, …
## $ Category        <chr> "Applicants", "Applicants", "Applicants", "Applicants"…
## $ Ethnicity       <chr> "International", "Unknown", "White", "Asian", "Chicano…
## $ `Perc FR`       <chr> "21.16%", "2.51%", "18.39%", "30.76%", "22.44%", "0.35…
## $ FilteredCountFR <dbl> 16522, 1959, 14360, 24024, 17526, 277, 3425, 78093, 15…
```

```r
dim(UC_admit)
```

```
## [1] 2160    6
```


```r
names(UC_admit)
```

```
## [1] "Campus"          "Academic_Yr"     "Category"        "Ethnicity"      
## [5] "Perc FR"         "FilteredCountFR"
```

```r
clean_UC_admit <- clean_names(UC_admit)
```


```r
names(clean_UC_admit)
```

```
## [1] "campus"            "academic_yr"       "category"         
## [4] "ethnicity"         "perc_fr"           "filtered_count_fr"
```


```r
is.na(UC_admit)
```

```
##         Campus Academic_Yr Category Ethnicity Perc FR FilteredCountFR
##    [1,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [2,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [3,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [4,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [5,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [6,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [7,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [8,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##    [9,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [10,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [11,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [12,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [13,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [14,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [15,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [16,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [17,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [18,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [19,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [20,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [21,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [22,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [23,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [24,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [25,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [26,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [27,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [28,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [29,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [30,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [31,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [32,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [33,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [34,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [35,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [36,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [37,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [38,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [39,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [40,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [41,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [42,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [43,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [44,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [45,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [46,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [47,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [48,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [49,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [50,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [51,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [52,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [53,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [54,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [55,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [56,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [57,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [58,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [59,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [60,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [61,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [62,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [63,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [64,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [65,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [66,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [67,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [68,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [69,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [70,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [71,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [72,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [73,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [74,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [75,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [76,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [77,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [78,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [79,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [80,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [81,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [82,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [83,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [84,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [85,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [86,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [87,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [88,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [89,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [90,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [91,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [92,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [93,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [94,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [95,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [96,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [97,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [98,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##   [99,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [100,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [101,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [102,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [103,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [104,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [105,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [106,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [107,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [108,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [109,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [110,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [111,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [112,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [113,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [114,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [115,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [116,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [117,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [118,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [119,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [120,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [121,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [122,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [123,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [124,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [125,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [126,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [127,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [128,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [129,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [130,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [131,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [132,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [133,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [134,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [135,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [136,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [137,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [138,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [139,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [140,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [141,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [142,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [143,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [144,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [145,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [146,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [147,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [148,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [149,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [150,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [151,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [152,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [153,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [154,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [155,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [156,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [157,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [158,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [159,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [160,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [161,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [162,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [163,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [164,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [165,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [166,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [167,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [168,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [169,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [170,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [171,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [172,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [173,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [174,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [175,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [176,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [177,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [178,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [179,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [180,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [181,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [182,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [183,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [184,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [185,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [186,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [187,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [188,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [189,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [190,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [191,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [192,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [193,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [194,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [195,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [196,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [197,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [198,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [199,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [200,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [201,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [202,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [203,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [204,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [205,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [206,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [207,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [208,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [209,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [210,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [211,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [212,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [213,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [214,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [215,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [216,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [217,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [218,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [219,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [220,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [221,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [222,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [223,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [224,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [225,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [226,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [227,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [228,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [229,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [230,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [231,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [232,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [233,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [234,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [235,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [236,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [237,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [238,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [239,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [240,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [241,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [242,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [243,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [244,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [245,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [246,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [247,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [248,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [249,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [250,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [251,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [252,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [253,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [254,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [255,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [256,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [257,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [258,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [259,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [260,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [261,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [262,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [263,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [264,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [265,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [266,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [267,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [268,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [269,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [270,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [271,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [272,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [273,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [274,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [275,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [276,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [277,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [278,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [279,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [280,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [281,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [282,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [283,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [284,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [285,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [286,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [287,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [288,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [289,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [290,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [291,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [292,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [293,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [294,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [295,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [296,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [297,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [298,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [299,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [300,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [301,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [302,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [303,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [304,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [305,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [306,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [307,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [308,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [309,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [310,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [311,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [312,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [313,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [314,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [315,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [316,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [317,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [318,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [319,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [320,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [321,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [322,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [323,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [324,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [325,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [326,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [327,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [328,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [329,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [330,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [331,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [332,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [333,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [334,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [335,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [336,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [337,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [338,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [339,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [340,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [341,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [342,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [343,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [344,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [345,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [346,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [347,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [348,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [349,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [350,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [351,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [352,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [353,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [354,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [355,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [356,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [357,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [358,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [359,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [360,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [361,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [362,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [363,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [364,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [365,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [366,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [367,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [368,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [369,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [370,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [371,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [372,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [373,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [374,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [375,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [376,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [377,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [378,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [379,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [380,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [381,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [382,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [383,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [384,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [385,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [386,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [387,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [388,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [389,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [390,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [391,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [392,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [393,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [394,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [395,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [396,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [397,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [398,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [399,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [400,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [401,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [402,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [403,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [404,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [405,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [406,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [407,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [408,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [409,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [410,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [411,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [412,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [413,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [414,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [415,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [416,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [417,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [418,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [419,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [420,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [421,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [422,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [423,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [424,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [425,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [426,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [427,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [428,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [429,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [430,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [431,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [432,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [433,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [434,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [435,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [436,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [437,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [438,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [439,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [440,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [441,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [442,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [443,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [444,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [445,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [446,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [447,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [448,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [449,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [450,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [451,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [452,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [453,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [454,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [455,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [456,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [457,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [458,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [459,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [460,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [461,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [462,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [463,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [464,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [465,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [466,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [467,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [468,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [469,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [470,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [471,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [472,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [473,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [474,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [475,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [476,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [477,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [478,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [479,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [480,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [481,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [482,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [483,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [484,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [485,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [486,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [487,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [488,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [489,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [490,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [491,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [492,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [493,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [494,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [495,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [496,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [497,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [498,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [499,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [500,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [501,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [502,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [503,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [504,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [505,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [506,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [507,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [508,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [509,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [510,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [511,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [512,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [513,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [514,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [515,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [516,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [517,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [518,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [519,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [520,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [521,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [522,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [523,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [524,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [525,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [526,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [527,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [528,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [529,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [530,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [531,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [532,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [533,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [534,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [535,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [536,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [537,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [538,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [539,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [540,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [541,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [542,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [543,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [544,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [545,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [546,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [547,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [548,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [549,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [550,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [551,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [552,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [553,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [554,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [555,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [556,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [557,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [558,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [559,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [560,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [561,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [562,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [563,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [564,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [565,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [566,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [567,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [568,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [569,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [570,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [571,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [572,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [573,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [574,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [575,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [576,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [577,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [578,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [579,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [580,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [581,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [582,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [583,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [584,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [585,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [586,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [587,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [588,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [589,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [590,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [591,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [592,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [593,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [594,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [595,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [596,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [597,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [598,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [599,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [600,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [601,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [602,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [603,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [604,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [605,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [606,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [607,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [608,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [609,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [610,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [611,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [612,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [613,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [614,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [615,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [616,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [617,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [618,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [619,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [620,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [621,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [622,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [623,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [624,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [625,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [626,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [627,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [628,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [629,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [630,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [631,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [632,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [633,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [634,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [635,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [636,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [637,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [638,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [639,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [640,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [641,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [642,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [643,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [644,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [645,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [646,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [647,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [648,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [649,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [650,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [651,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [652,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [653,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [654,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [655,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [656,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [657,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [658,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [659,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [660,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [661,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [662,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [663,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [664,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [665,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [666,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [667,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [668,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [669,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [670,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [671,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [672,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [673,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [674,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [675,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [676,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [677,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [678,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [679,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [680,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [681,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [682,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [683,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [684,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [685,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [686,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [687,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [688,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [689,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [690,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [691,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [692,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [693,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [694,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [695,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [696,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [697,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [698,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [699,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [700,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [701,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [702,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [703,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [704,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [705,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [706,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [707,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [708,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [709,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [710,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [711,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [712,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [713,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [714,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [715,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [716,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [717,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [718,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [719,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [720,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [721,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [722,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [723,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [724,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [725,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [726,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [727,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [728,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [729,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [730,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [731,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [732,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [733,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [734,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [735,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [736,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [737,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [738,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [739,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [740,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [741,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [742,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [743,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [744,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [745,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [746,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [747,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [748,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [749,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [750,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [751,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [752,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [753,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [754,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [755,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [756,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [757,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [758,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [759,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [760,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [761,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [762,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [763,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [764,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [765,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [766,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [767,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [768,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [769,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [770,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [771,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [772,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [773,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [774,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [775,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [776,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [777,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [778,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [779,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [780,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [781,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [782,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [783,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [784,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [785,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [786,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [787,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [788,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [789,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [790,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [791,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [792,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [793,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [794,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [795,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [796,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [797,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [798,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [799,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [800,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [801,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [802,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [803,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [804,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [805,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [806,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [807,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [808,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [809,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [810,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [811,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [812,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [813,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [814,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [815,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [816,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [817,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [818,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [819,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [820,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [821,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [822,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [823,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [824,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [825,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [826,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [827,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [828,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [829,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [830,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [831,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [832,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [833,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [834,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [835,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [836,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [837,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [838,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [839,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [840,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [841,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [842,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [843,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [844,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [845,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [846,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [847,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [848,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [849,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [850,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [851,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [852,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [853,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [854,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [855,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [856,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [857,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [858,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [859,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [860,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [861,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [862,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [863,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [864,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [865,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [866,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [867,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [868,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [869,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [870,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [871,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [872,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [873,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [874,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [875,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [876,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [877,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [878,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [879,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [880,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [881,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [882,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [883,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [884,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [885,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [886,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [887,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [888,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [889,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [890,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [891,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [892,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [893,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [894,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [895,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [896,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [897,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [898,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [899,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [900,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [901,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [902,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [903,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [904,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [905,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [906,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [907,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [908,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [909,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [910,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [911,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [912,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [913,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [914,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [915,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [916,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [917,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [918,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [919,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [920,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [921,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [922,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [923,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [924,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [925,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [926,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [927,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [928,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [929,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [930,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [931,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [932,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [933,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [934,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [935,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [936,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [937,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [938,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [939,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [940,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [941,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [942,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [943,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [944,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [945,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [946,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [947,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [948,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [949,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [950,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [951,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [952,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [953,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [954,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [955,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [956,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [957,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [958,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [959,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [960,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [961,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [962,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [963,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [964,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [965,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [966,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [967,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [968,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [969,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [970,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [971,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [972,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [973,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [974,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [975,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [976,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [977,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [978,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [979,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [980,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [981,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [982,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [983,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [984,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [985,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [986,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [987,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [988,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [989,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [990,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [991,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [992,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [993,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [994,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [995,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [996,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [997,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [998,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
##  [999,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1000,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1001,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1002,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1003,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1004,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1005,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1006,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1007,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1008,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1009,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1010,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1011,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1012,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1013,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1014,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1015,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1016,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1017,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1018,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1019,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1020,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1021,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1022,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1023,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1024,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1025,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1026,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1027,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1028,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1029,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1030,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1031,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1032,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1033,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1034,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1035,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1036,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1037,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1038,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1039,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1040,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1041,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1042,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1043,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1044,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1045,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1046,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1047,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1048,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1049,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1050,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1051,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1052,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1053,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1054,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1055,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1056,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1057,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1058,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1059,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1060,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1061,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1062,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1063,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1064,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1065,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1066,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1067,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1068,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1069,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1070,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1071,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1072,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1073,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1074,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1075,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1076,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1077,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1078,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1079,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1080,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1081,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1082,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1083,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1084,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1085,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1086,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1087,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1088,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1089,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1090,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1091,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1092,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1093,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1094,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1095,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1096,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1097,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1098,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1099,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1100,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1101,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1102,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1103,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1104,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1105,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1106,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1107,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1108,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1109,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1110,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1111,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1112,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1113,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1114,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1115,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1116,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1117,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1118,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1119,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1120,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1121,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1122,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1123,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1124,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1125,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1126,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1127,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1128,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1129,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1130,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1131,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1132,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1133,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1134,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1135,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1136,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1137,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1138,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1139,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1140,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1141,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1142,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1143,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1144,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1145,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1146,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1147,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1148,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1149,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1150,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1151,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1152,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1153,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1154,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1155,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1156,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1157,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1158,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1159,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1160,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1161,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1162,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1163,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1164,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1165,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1166,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1167,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1168,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1169,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1170,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1171,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1172,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1173,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1174,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1175,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1176,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1177,]  FALSE       FALSE    FALSE     FALSE    TRUE            TRUE
## [1178,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1179,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1180,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1181,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1182,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1183,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1184,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1185,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1186,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1187,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1188,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1189,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1190,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1191,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1192,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1193,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1194,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1195,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1196,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1197,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1198,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1199,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1200,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1201,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1202,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1203,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1204,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1205,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1206,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1207,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1208,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1209,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1210,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1211,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1212,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1213,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1214,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1215,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1216,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1217,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1218,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1219,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1220,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1221,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1222,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1223,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1224,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1225,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1226,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1227,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1228,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1229,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1230,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1231,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1232,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1233,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1234,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1235,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1236,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1237,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1238,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1239,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1240,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1241,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1242,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1243,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1244,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1245,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1246,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1247,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1248,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1249,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1250,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1251,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1252,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1253,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1254,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1255,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1256,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1257,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1258,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1259,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1260,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1261,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1262,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1263,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1264,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1265,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1266,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1267,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1268,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1269,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1270,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1271,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1272,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1273,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1274,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1275,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1276,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1277,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1278,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1279,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1280,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1281,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1282,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1283,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1284,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1285,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1286,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1287,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1288,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1289,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1290,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1291,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1292,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1293,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1294,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1295,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1296,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1297,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1298,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1299,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1300,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1301,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1302,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1303,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1304,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1305,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1306,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1307,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1308,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1309,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1310,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1311,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1312,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1313,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1314,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1315,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1316,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1317,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1318,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1319,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1320,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1321,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1322,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1323,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1324,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1325,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1326,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1327,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1328,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1329,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1330,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1331,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1332,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1333,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1334,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1335,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1336,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1337,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1338,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1339,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1340,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1341,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1342,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1343,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1344,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1345,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1346,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1347,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1348,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1349,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1350,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1351,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1352,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1353,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1354,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1355,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1356,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1357,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1358,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1359,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1360,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1361,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1362,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1363,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1364,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1365,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1366,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1367,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1368,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1369,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1370,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1371,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1372,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1373,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1374,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1375,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1376,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1377,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1378,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1379,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1380,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1381,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1382,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1383,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1384,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1385,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1386,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1387,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1388,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1389,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1390,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1391,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1392,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1393,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1394,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1395,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1396,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1397,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1398,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1399,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1400,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1401,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1402,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1403,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1404,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1405,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1406,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1407,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1408,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1409,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1410,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1411,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1412,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1413,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1414,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1415,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1416,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1417,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1418,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1419,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1420,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1421,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1422,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1423,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1424,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1425,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1426,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1427,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1428,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1429,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1430,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1431,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1432,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1433,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1434,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1435,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1436,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1437,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1438,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1439,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1440,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1441,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1442,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1443,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1444,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1445,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1446,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1447,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1448,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1449,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1450,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1451,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1452,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1453,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1454,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1455,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1456,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1457,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1458,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1459,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1460,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1461,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1462,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1463,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1464,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1465,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1466,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1467,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1468,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1469,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1470,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1471,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1472,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1473,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1474,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1475,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1476,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1477,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1478,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1479,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1480,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1481,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1482,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1483,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1484,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1485,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1486,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1487,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1488,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1489,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1490,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1491,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1492,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1493,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1494,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1495,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1496,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1497,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1498,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1499,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1500,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1501,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1502,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1503,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1504,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1505,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1506,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1507,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1508,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1509,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1510,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1511,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1512,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1513,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1514,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1515,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1516,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1517,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1518,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1519,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1520,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1521,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1522,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1523,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1524,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1525,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1526,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1527,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1528,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1529,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1530,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1531,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1532,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1533,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1534,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1535,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1536,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1537,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1538,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1539,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1540,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1541,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1542,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1543,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1544,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1545,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1546,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1547,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1548,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1549,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1550,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1551,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1552,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1553,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1554,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1555,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1556,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1557,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1558,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1559,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1560,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1561,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1562,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1563,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1564,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1565,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1566,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1567,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1568,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1569,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1570,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1571,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1572,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1573,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1574,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1575,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1576,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1577,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1578,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1579,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1580,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1581,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1582,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1583,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1584,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1585,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1586,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1587,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1588,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1589,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1590,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1591,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1592,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1593,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1594,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1595,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1596,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1597,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1598,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1599,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1600,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1601,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1602,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1603,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1604,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1605,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1606,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1607,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1608,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1609,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1610,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1611,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1612,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1613,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1614,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1615,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1616,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1617,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1618,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1619,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1620,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1621,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1622,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1623,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1624,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1625,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1626,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1627,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1628,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1629,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1630,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1631,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1632,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1633,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1634,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1635,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1636,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1637,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1638,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1639,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1640,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1641,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1642,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1643,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1644,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1645,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1646,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1647,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1648,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1649,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1650,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1651,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1652,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1653,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1654,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1655,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1656,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1657,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1658,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1659,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1660,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1661,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1662,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1663,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1664,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1665,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1666,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1667,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1668,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1669,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1670,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1671,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1672,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1673,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1674,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1675,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1676,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1677,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1678,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1679,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1680,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1681,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1682,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1683,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1684,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1685,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1686,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1687,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1688,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1689,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1690,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1691,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1692,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1693,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1694,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1695,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1696,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1697,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1698,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1699,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1700,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1701,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1702,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1703,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1704,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1705,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1706,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1707,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1708,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1709,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1710,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1711,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1712,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1713,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1714,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1715,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1716,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1717,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1718,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1719,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1720,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1721,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1722,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1723,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1724,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1725,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1726,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1727,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1728,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1729,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1730,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1731,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1732,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1733,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1734,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1735,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1736,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1737,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1738,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1739,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1740,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1741,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1742,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1743,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1744,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1745,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1746,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1747,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1748,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1749,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1750,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1751,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1752,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1753,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1754,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1755,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1756,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1757,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1758,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1759,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1760,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1761,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1762,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1763,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1764,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1765,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1766,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1767,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1768,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1769,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1770,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1771,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1772,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1773,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1774,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1775,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1776,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1777,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1778,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1779,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1780,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1781,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1782,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1783,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1784,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1785,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1786,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1787,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1788,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1789,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1790,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1791,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1792,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1793,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1794,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1795,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1796,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1797,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1798,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1799,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1800,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1801,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1802,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1803,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1804,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1805,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1806,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1807,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1808,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1809,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1810,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1811,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1812,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1813,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1814,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1815,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1816,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1817,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1818,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1819,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1820,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1821,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1822,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1823,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1824,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1825,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1826,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1827,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1828,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1829,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1830,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1831,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1832,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1833,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1834,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1835,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1836,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1837,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1838,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1839,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1840,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1841,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1842,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1843,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1844,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1845,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1846,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1847,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1848,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1849,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1850,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1851,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1852,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1853,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1854,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1855,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1856,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1857,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1858,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1859,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1860,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1861,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1862,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1863,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1864,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1865,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1866,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1867,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1868,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1869,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1870,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1871,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1872,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1873,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1874,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1875,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1876,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1877,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1878,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1879,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1880,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1881,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1882,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1883,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1884,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1885,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1886,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1887,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1888,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1889,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1890,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1891,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1892,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1893,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1894,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1895,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1896,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1897,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1898,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1899,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1900,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1901,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1902,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1903,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1904,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1905,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1906,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1907,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1908,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1909,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1910,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1911,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1912,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1913,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1914,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1915,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1916,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1917,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1918,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1919,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1920,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1921,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1922,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1923,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1924,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1925,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1926,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1927,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1928,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1929,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1930,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1931,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1932,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1933,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1934,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1935,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1936,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1937,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1938,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1939,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1940,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1941,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1942,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1943,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1944,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1945,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1946,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1947,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1948,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1949,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1950,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1951,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1952,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1953,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1954,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1955,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1956,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1957,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1958,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1959,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1960,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1961,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1962,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1963,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1964,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1965,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1966,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1967,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1968,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1969,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1970,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1971,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1972,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1973,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1974,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1975,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1976,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1977,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1978,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1979,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1980,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1981,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1982,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1983,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1984,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1985,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1986,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1987,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1988,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1989,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1990,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1991,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1992,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1993,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1994,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1995,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1996,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1997,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1998,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [1999,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2000,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2001,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2002,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2003,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2004,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2005,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2006,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2007,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2008,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2009,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2010,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2011,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2012,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2013,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2014,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2015,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2016,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2017,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2018,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2019,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2020,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2021,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2022,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2023,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2024,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2025,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2026,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2027,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2028,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2029,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2030,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2031,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2032,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2033,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2034,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2035,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2036,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2037,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2038,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2039,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2040,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2041,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2042,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2043,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2044,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2045,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2046,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2047,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2048,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2049,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2050,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2051,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2052,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2053,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2054,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2055,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2056,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2057,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2058,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2059,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2060,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2061,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2062,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2063,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2064,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2065,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2066,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2067,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2068,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2069,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2070,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2071,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2072,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2073,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2074,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2075,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2076,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2077,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2078,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2079,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2080,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2081,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2082,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2083,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2084,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2085,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2086,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2087,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2088,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2089,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2090,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2091,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2092,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2093,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2094,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2095,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2096,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2097,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2098,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2099,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2100,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2101,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2102,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2103,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2104,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2105,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2106,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2107,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2108,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2109,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2110,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2111,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2112,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2113,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2114,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2115,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2116,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2117,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2118,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2119,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2120,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2121,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2122,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2123,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2124,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2125,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2126,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2127,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2128,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2129,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2130,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2131,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2132,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2133,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2134,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2135,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2136,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2137,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2138,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2139,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2140,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2141,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2142,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2143,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2144,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2145,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2146,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2147,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2148,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2149,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2150,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2151,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2152,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2153,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2154,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2155,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2156,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2157,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2158,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2159,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
## [2160,]  FALSE       FALSE    FALSE     FALSE   FALSE           FALSE
```

**2. The president of UC has asked you to build a shiny app that shows admissions by ethnicity across all UC campuses. Your app should allow users to explore year, campus, and admit category as interactive variables. Use shiny dashboard and try to incorporate the aesthetics you have learned in ggplot to make the app neat and clean.*



```r
clean_UC_admit %>% 
  count(category)
```

```
## # A tibble: 3 × 2
##   category       n
##   <chr>      <int>
## 1 Admits       720
## 2 Applicants   720
## 3 Enrollees    720
```


```r
clean_UC_admit %>% 
  filter(ethnicity != "All" & ethnicity !="Unknown") %>% 
  ggplot(aes(x=ethnicity, y= perc_fr, fill=ethnicity))+
  geom_col()
```

![](lab13_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
library(shiny)
ui <- dashboardPage(
  dashboardHeader(title = "Admissions Ethnicity By Year, Campus, and Admit Category"),
  dashboardSidebar(disable=T),
  dashboardBody(
  fluidRow(
  box(title = "Plot Options", width = 3,
      selectInput("x", " Select Year:", 
                  choices=c("2019","2018","2017","2016","2015","2014","2013", "2012","2011","2010"),selected="2019"),
      selectInput("y", " Select Campus:", 
                  choices=c("Berkeley", "Davis", "Irvine", "Los_Angeles", "Merced", "Riverside", "San_Diego", "Santa_Barbara", "Santa_Cruz"),selected="Berkley"),
      selectInput("z", " Select Admit Category:", 
                  choices=c("Admits", "Applicants", "Enrollees"),selected="Admits")
  ),
    box(title = "Admissions Ethnicity By Year, Campus, and Admit Category", width = 7,
   plotOutput("plot", width = "600px", height = "500px")
    )
    )
    )
)
  


server <- function(input, output, session) {
  output$plot <- renderPlot({
  clean_UC_admit %>% 
       filter(ethnicity != "All" & ethnicity !="Unknown") %>% 
      filter(academic_yr==input$x) %>% 
      filter(campus==input$y) %>% 
      filter(category==input$z) %>% 
      ggplot(aes(x=ethnicity, y= perc_fr, fill=ethnicity))+
      geom_col()
  })
session$onSessionEnded(stopApp)
}

shinyApp(ui, server)
```

```r
server <- function(input, output, session) {
  output$plot <- renderPlot({
clean_UC_admit %>% 
  filter(ethnicity != "All" & ethnicity !="Unknown") %>% 
    filter(academic_yr==input$x) %>% 
  ggplot(aes(x=ethnicity, y= perc_fr, fill=ethnicity))+
  geom_col()
  
  })
} 
```



**3. Make alternate version of your app above by tracking enrollment at a campus over all of the represented years while allowing users to interact with campus, category, and ethnicity.**

```r
clean_UC_admit %>% 
  count(academic_yr)
```

```
## # A tibble: 10 × 2
##    academic_yr     n
##          <dbl> <int>
##  1        2010   216
##  2        2011   216
##  3        2012   216
##  4        2013   216
##  5        2014   216
##  6        2015   216
##  7        2016   216
##  8        2017   216
##  9        2018   216
## 10        2019   216
```



```r
academic_yr <- as.factor("academic_yr")
library(shiny)
ui <- dashboardPage(
  dashboardHeader(title = "UC Campus Admissions By Ethnicity, Campus, and Admit Category"),
  dashboardSidebar(disable=T),
  dashboardBody(
  fluidRow(
  box(title = "Plot Options", width = 3,
      selectInput("x", " Select Ethnicity:", 
                  choices=c("African American","American Indian","Asian","Chicano/Latino","International","White"),selected="African American"),
      selectInput("y", " Select Campus:", 
                  choices=c("Berkeley", "Davis", "Irvine", "Los_Angeles", "Merced", "Riverside", "San_Diego", "Santa_Barbara", "Santa_Cruz"),selected="Berkley"),
      selectInput("z", " Select Admit Category:", 
                  choices=c("Admits", "Applicants", "Enrollees"),selected="Admits"),
  ),
    box(title = "UC Campus Admissions By Ethnicity, Campus, and Admit Category", width = 7,
   plotOutput("plot", width = "600px", height = "500px")
    )
    )
    )
)
  


server <- function(input, output, session) {
  output$plot <- renderPlot({
clean_UC_admit %>%
  filter(ethnicity==input$x) %>% 
  filter(campus==input$y) %>% 
  filter(category==input$z) %>% 
  ggplot(aes(x=academic_yr,y=filtered_count_fr, fill=academic_yr))+
  geom_col()
  })
session$onSessionEnded(stopApp)
}

shinyApp(ui, server)
```

`<div style="width: 100% ; height: 400px ; text-align: center; box-sizing: border-box; -moz-box-sizing: border-box; -webkit-box-sizing: border-box;" class="muted well">Shiny applications not supported in static R Markdown documents</div>`{=html}


 
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
