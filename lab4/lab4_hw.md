---
title: "Lab 4 Homework"
author: "Maggie Bauer"
date: "2022-01-15"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
```

```
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
homerange
```

```
## # A tibble: 569 × 24
##    taxon  common.name   class   order   family genus species primarymethod N    
##    <chr>  <chr>         <chr>   <chr>   <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake … american eel  actino… anguil… angui… angu… rostra… telemetry     16   
##  2 river… blacktail re… actino… cyprin… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 river… central ston… actino… cyprin… cypri… camp… anomal… mark-recaptu… 20   
##  4 river… rosyside dace actino… cyprin… cypri… clin… fundul… mark-recaptu… 26   
##  5 river… longnose dace actino… cyprin… cypri… rhin… catara… mark-recaptu… 17   
##  6 river… muskellunge   actino… esocif… esoci… esox  masqui… telemetry     5    
##  7 marin… pollack       actino… gadifo… gadid… poll… pollac… telemetry     2    
##  8 marin… saithe        actino… gadifo… gadid… poll… virens  telemetry     2    
##  9 marin… lined surgeo… actino… percif… acant… acan… lineat… direct obser… <NA> 
## 10 marin… orangespine … actino… percif… acant… naso  litura… telemetry     8    
## # … with 559 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```
 
**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```

```r
names(homerange) 
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
class(homerange$taxon)
```

```
## [1] "character"
```

```r
homerange$taxon <- as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```

```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
class(homerange$order)
```

```
## [1] "character"
```

```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes\xa0" "tinamiformes"
```
**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
select(homerange, taxon)
```

```
## # A tibble: 569 × 1
##    taxon        
##    <fct>        
##  1 lake fishes  
##  2 river fishes 
##  3 river fishes 
##  4 river fishes 
##  5 river fishes 
##  6 river fishes 
##  7 marine fishes
##  8 marine fishes
##  9 marine fishes
## 10 marine fishes
## # … with 559 more rows
```

```r
taxa <- select(homerange, taxon, common.name, class, order, family, genus, species)
taxa
```

```
## # A tibble: 569 × 7
##    taxon         common.name             class   order   family   genus  species
##    <fct>         <chr>                   <chr>   <fct>   <chr>    <chr>  <chr>  
##  1 lake fishes   american eel            actino… anguil… anguill… angui… rostra…
##  2 river fishes  blacktail redhorse      actino… cyprin… catosto… moxos… poecil…
##  3 river fishes  central stoneroller     actino… cyprin… cyprini… campo… anomal…
##  4 river fishes  rosyside dace           actino… cyprin… cyprini… clino… fundul…
##  5 river fishes  longnose dace           actino… cyprin… cyprini… rhini… catara…
##  6 river fishes  muskellunge             actino… esocif… esocidae esox   masqui…
##  7 marine fishes pollack                 actino… gadifo… gadidae  polla… pollac…
##  8 marine fishes saithe                  actino… gadifo… gadidae  polla… virens 
##  9 marine fishes lined surgeonfish       actino… percif… acanthu… acant… lineat…
## 10 marine fishes orangespine unicornfish actino… percif… acanthu… naso   litura…
## # … with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```


**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
all_carn <- filter(homerange , trophic.guild == "carnivore")
all_carn
```

```
## # A tibble: 342 × 24
##    taxon   common.name   class   order  family genus species primarymethod N    
##    <fct>   <chr>         <chr>   <fct>  <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake f… american eel  actino… angui… angui… angu… rostra… telemetry     16   
##  2 river … blacktail re… actino… cypri… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 river … central ston… actino… cypri… cypri… camp… anomal… mark-recaptu… 20   
##  4 river … rosyside dace actino… cypri… cypri… clin… fundul… mark-recaptu… 26   
##  5 river … longnose dace actino… cypri… cypri… rhin… catara… mark-recaptu… 17   
##  6 river … muskellunge   actino… esoci… esoci… esox  masqui… telemetry     5    
##  7 marine… pollack       actino… gadif… gadid… poll… pollac… telemetry     2    
##  8 marine… saithe        actino… gadif… gadid… poll… virens  telemetry     2    
##  9 marine… giant treval… actino… perci… caran… cara… ignobi… telemetry     4    
## 10 lake f… rock bass     actino… perci… centr… ambl… rupest… mark-recaptu… 16   
## # … with 332 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

```r
all_herb <- filter(homerange, trophic.guild == "herbivore")
all_herb
```

```
## # A tibble: 227 × 24
##    taxon  common.name   class   order  family  genus species primarymethod N    
##    <fct>  <chr>         <chr>   <fct>  <chr>   <chr> <chr>   <chr>         <chr>
##  1 marin… lined surgeo… actino… perci… acanth… acan… lineat… direct obser… <NA> 
##  2 marin… orangespine … actino… perci… acanth… naso  litura… telemetry     8    
##  3 marin… bluespine un… actino… perci… acanth… naso  unicor… telemetry     7    
##  4 marin… redlip blenny actino… perci… blenni… ophi… atlant… direct obser… 20   
##  5 marin… bermuda chub  actino… perci… kyphos… kyph… sectat… telemetry     11   
##  6 marin… cherubfish    actino… perci… pomaca… cent… argi    direct obser… <NA> 
##  7 marin… damselfish    actino… perci… pomace… chro… chromis direct obser… <NA> 
##  8 marin… twinspot dam… actino… perci… pomace… chry… biocel… direct obser… 18   
##  9 marin… wards damsel  actino… perci… pomace… poma… wardi   direct obser… <NA> 
## 10 marin… australian g… actino… perci… pomace… steg… apical… direct obser… <NA> 
## # … with 217 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```


**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  


```r
newall_carn <- all_carn[ ,13]
```

```r
colMeans(newall_carn, na.rm=TRUE)
```

```
## mean.hra.m2 
##    13039918
```

```r
newall_herb <- all_herb[ ,13]
```

```r
colMeans(newall_herb, na.rm=TRUE)
```

```
## mean.hra.m2 
##    34137012
```

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer <- select(homerange, mean.mass.g, log10.mass, family, genus, species)
deer
```

```
## # A tibble: 569 × 5
##    mean.mass.g log10.mass family       genus       species    
##          <dbl>      <dbl> <chr>        <chr>       <chr>      
##  1        887       2.95  anguillidae  anguilla    rostrata   
##  2        562       2.75  catostomidae moxostoma   poecilura  
##  3         34       1.53  cyprinidae   campostoma  anomalum   
##  4          4       0.602 cyprinidae   clinostomus funduloides
##  5          4       0.602 cyprinidae   rhinichthys cataractae 
##  6       3525       3.55  esocidae     esox        masquinongy
##  7        737.      2.87  gadidae      pollachius  pollachius 
##  8        449.      2.65  gadidae      pollachius  virens     
##  9        109.      2.04  acanthuridae acanthurus  lineatus   
## 10        772.      2.89  acanthuridae naso        lituratus  
## # … with 559 more rows
```

```r
deer_1 <- filter(homerange, family == "cervidae")
deer_1
```

```
## # A tibble: 12 × 24
##    taxon   common.name   class  order   family genus species primarymethod N    
##    <fct>   <chr>         <chr>  <fct>   <chr>  <chr> <chr>   <chr>         <chr>
##  1 mammals moose         mamma… artiod… cervi… alces alces   telemetry*    <NA> 
##  2 mammals chital        mamma… artiod… cervi… axis  axis    telemetry*    <NA> 
##  3 mammals roe deer      mamma… artiod… cervi… capr… capreo… telemetry*    <NA> 
##  4 mammals red deer      mamma… artiod… cervi… cerv… elaphus telemetry*    <NA> 
##  5 mammals sika deer     mamma… artiod… cervi… cerv… nippon  telemetry*    <NA> 
##  6 mammals fallow deer   mamma… artiod… cervi… dama  dama    telemetry*    <NA> 
##  7 mammals Reeves's mun… mamma… artiod… cervi… munt… reevesi telemetry*    <NA> 
##  8 mammals mule deer     mamma… artiod… cervi… odoc… hemion… telemetry*    <NA> 
##  9 mammals white-tailed… mamma… artiod… cervi… odoc… virgin… telemetry*    <NA> 
## 10 mammals pampas deer   mamma… artiod… cervi… ozot… bezoar… telemetry*    <NA> 
## 11 mammals pudu          mamma… artiod… cervi… pudu  puda    telemetry*    <NA> 
## 12 mammals reindeer      mamma… artiod… cervi… rang… tarand… telemetry*    <NA> 
## # … with 15 more variables: mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <dbl>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```

```r
arrange(deer_1, log10.mass)
```

```
## # A tibble: 12 × 24
##    taxon   common.name   class  order   family genus species primarymethod N    
##    <fct>   <chr>         <chr>  <fct>   <chr>  <chr> <chr>   <chr>         <chr>
##  1 mammals pudu          mamma… artiod… cervi… pudu  puda    telemetry*    <NA> 
##  2 mammals Reeves's mun… mamma… artiod… cervi… munt… reevesi telemetry*    <NA> 
##  3 mammals roe deer      mamma… artiod… cervi… capr… capreo… telemetry*    <NA> 
##  4 mammals sika deer     mamma… artiod… cervi… cerv… nippon  telemetry*    <NA> 
##  5 mammals pampas deer   mamma… artiod… cervi… ozot… bezoar… telemetry*    <NA> 
##  6 mammals mule deer     mamma… artiod… cervi… odoc… hemion… telemetry*    <NA> 
##  7 mammals chital        mamma… artiod… cervi… axis  axis    telemetry*    <NA> 
##  8 mammals fallow deer   mamma… artiod… cervi… dama  dama    telemetry*    <NA> 
##  9 mammals white-tailed… mamma… artiod… cervi… odoc… virgin… telemetry*    <NA> 
## 10 mammals reindeer      mamma… artiod… cervi… rang… tarand… telemetry*    <NA> 
## 11 mammals red deer      mamma… artiod… cervi… cerv… elaphus telemetry*    <NA> 
## 12 mammals moose         mamma… artiod… cervi… alces alces   telemetry*    <NA> 
## # … with 15 more variables: mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <dbl>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```

Moose 

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

```r
snakes <- filter(homerange, family == "colubridae" |  family == "elapidae" |  family == "viperidae" )
snakes
```

```
## # A tibble: 40 × 24
##    taxon  common.name   class  order  family genus species   primarymethod N    
##    <fct>  <chr>         <chr>  <fct>  <chr>  <chr> <chr>     <chr>         <chr>
##  1 snakes western worm… repti… squam… colub… carp… vermis    radiotag      1    
##  2 snakes eastern worm… repti… squam… colub… carp… viridis   radiotag      10   
##  3 snakes racer         repti… squam… colub… colu… constric… telemetry     15   
##  4 snakes yellow belli… repti… squam… colub… colu… constric… telemetry     12   
##  5 snakes ringneck sna… repti… squam… colub… diad… punctatus mark-recaptu… <NA> 
##  6 snakes eastern indi… repti… squam… colub… drym… couperi   telemetry     1    
##  7 snakes great plains… repti… squam… colub… elap… guttata … telemetry     12   
##  8 snakes western rats… repti… squam… colub… elap… obsoleta  telemetry     18   
##  9 snakes hognose snake repti… squam… colub… hete… platirhi… telemetry     8    
## 10 snakes European whi… repti… squam… colub… hier… viridifl… telemetry     32   
## # … with 30 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

```r
arrange(snakes, mean.hra.m2)
```

```
## # A tibble: 40 × 24
##    taxon  common.name   class  order  family  genus  species primarymethod N    
##    <fct>  <chr>         <chr>  <fct>  <chr>   <chr>  <chr>   <chr>         <chr>
##  1 snakes namaqua dwar… repti… squam… viperi… bitis  schnei… telemetry     11   
##  2 snakes eastern worm… repti… squam… colubr… carph… viridis radiotag      10   
##  3 snakes butlers gart… repti… squam… colubr… thamn… butleri mark-recaptu… 1    
##  4 snakes western worm… repti… squam… colubr… carph… vermis  radiotag      1    
##  5 snakes snubnosed vi… repti… squam… viperi… vipera latast… telemetry     7    
##  6 snakes chinese pit … repti… squam… viperi… gloyd… shedao… telemetry     16   
##  7 snakes ringneck sna… repti… squam… colubr… diado… puncta… mark-recaptu… <NA> 
##  8 snakes cottonmouth   repti… squam… viperi… agkis… pisciv… telemetry     15   
##  9 snakes redbacked ra… repti… squam… colubr… oocat… rufodo… telemetry     21   
## 10 snakes gopher snake  repti… squam… colubr… pituo… cateni… telemetry     4    
## # … with 30 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```
Namaqua Dwarf Adder	has the smallest homerange. It is venomous and is the smallest viper. It's habitat is a small area of coastal sand dunes of Namibia. 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
