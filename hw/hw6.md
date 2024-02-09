---
title: "Homework 6"
author: "Maya Ziebarth"
date: "2024-02-09"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv") 
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
fisheries <- clean_names(fisheries)
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ country                 <chr> "Albania", "Albania", "Albania", "Albania", "A…
## $ common_name             <chr> "Angelsharks, sand devils nei", "Atlantic boni…
## $ isscaap_group_number    <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, 57…
## $ isscaap_taxonomic_group <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, bi…
## $ asfis_species_number    <chr> "10903XXXXX", "1750100101", "17710001XX", "228…
## $ asfis_species_name      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp",…
## $ fao_major_fishing_area  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37…
## $ measure                 <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Qua…
## $ x1950                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1951                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1952                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1953                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1954                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1955                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1956                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1957                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1958                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1959                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1960                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1961                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1962                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1963                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1964                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1965                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1966                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1967                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1968                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1969                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1970                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1971                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1972                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1973                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1974                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1975                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1976                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1977                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1978                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1979                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1980                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1981                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1982                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ x1983                   <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, NA,…
## $ x1984                   <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, NA,…
## $ x1985                   <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, NA,…
## $ x1986                   <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, NA,…
## $ x1987                   <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, NA,…
## $ x1988                   <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, NA,…
## $ x1989                   <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, NA,…
## $ x1990                   <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, NA,…
## $ x1991                   <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, NA,…
## $ x1992                   <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, NA,…
## $ x1993                   <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA, N…
## $ x1994                   <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA, N…
## $ x1995                   <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30", …
## $ x1996                   <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA, "…
## $ x1997                   <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4", …
## $ x1998                   <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA, "…
## $ x1999                   <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA, "…
## $ x2000                   <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA, …
## $ x2001                   <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA, "…
## $ x2002                   <chr> "79", "24", NA, "34", "6", NA, "150", "84", NA…
## $ x2003                   <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA, "…
## $ x2004                   <chr> "4", "2", "2", "15", "1", "2", "76", "285", "1…
## $ x2005                   <chr> "68", "23", "4", "12", "5", "6", "68", "150", …
## $ x2006                   <chr> "55", "30", "7", "18", "8", "9", "86", "102", …
## $ x2007                   <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA, "…
## $ x2008                   <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA, "…
## $ x2009                   <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA, "…
## $ x2010                   <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA, …
## $ x2011                   <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "90…
## $ x2012                   <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, "1…
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries %>% 
  mutate_if(is.character, factor)
```

```
## # A tibble: 17,692 × 71
##    country common_name               isscaap_group_number isscaap_taxonomic_gr…¹
##    <fct>   <fct>                                    <dbl> <fct>                 
##  1 Albania Angelsharks, sand devils…                   38 Sharks, rays, chimaer…
##  2 Albania Atlantic bonito                             36 Tunas, bonitos, billf…
##  3 Albania Barracudas nei                              37 Miscellaneous pelagic…
##  4 Albania Blue and red shrimp                         45 Shrimps, prawns       
##  5 Albania Blue whiting(=Poutassou)                    32 Cods, hakes, haddocks 
##  6 Albania Bluefish                                    37 Miscellaneous pelagic…
##  7 Albania Bogue                                       33 Miscellaneous coastal…
##  8 Albania Caramote prawn                              45 Shrimps, prawns       
##  9 Albania Catsharks, nursehounds n…                   38 Sharks, rays, chimaer…
## 10 Albania Common cuttlefish                           57 Squids, cuttlefishes,…
## # ℹ 17,682 more rows
## # ℹ abbreviated name: ¹​isscaap_taxonomic_group
## # ℹ 67 more variables: asfis_species_number <fct>, asfis_species_name <fct>,
## #   fao_major_fishing_area <dbl>, measure <fct>, x1950 <fct>, x1951 <fct>,
## #   x1952 <fct>, x1953 <fct>, x1954 <fct>, x1955 <fct>, x1956 <fct>,
## #   x1957 <fct>, x1958 <fct>, x1959 <fct>, x1960 <fct>, x1961 <fct>,
## #   x1962 <fct>, x1963 <fct>, x1964 <fct>, x1965 <fct>, x1966 <fct>, …
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!  

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>% 
 summarize(distinct_countries = n_distinct(country))
```

```
## # A tibble: 1 × 1
##   distinct_countries
##                <int>
## 1                203
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
select(fisheries_tidy, "country", "isscaap_taxonomic_group", "asfis_species_name", "asfis_species_number", "year", "catch")
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_species_number  year
##    <chr>   <chr>                   <chr>              <chr>                <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1995
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1996
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1997
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1998
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1999
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2000
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2001
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2002
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2003
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2004
## # ℹ 376,761 more rows
## # ℹ 1 more variable: catch <dbl>
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>% 
  summarize(disincit_species=n_distinct(asfis_species_name))
```

```
## # A tibble: 1 × 1
##   disincit_species
##              <int>
## 1             1546
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  select(country, year, catch) %>% 
  filter(year==2000) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 8,793 × 3
##    country                   year catch
##    <chr>                    <dbl> <dbl>
##  1 China                     2000  9068
##  2 Peru                      2000  5717
##  3 Russian Federation        2000  5065
##  4 Viet Nam                  2000  4945
##  5 Chile                     2000  4299
##  6 China                     2000  3288
##  7 China                     2000  2782
##  8 United States of America  2000  2438
##  9 China                     2000  1234
## 10 Philippines               2000   999
## # ℹ 8,783 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>% 
  select(country, asfis_species_name, year, catch) %>% 
  filter(year>=1990 & year<=2000) %>% 
  filter(asfis_species_name=="Sardina pilchardus") %>% 
  arrange(desc(catch))
```

```
## # A tibble: 336 × 4
##    country            asfis_species_name  year catch
##    <chr>              <chr>              <dbl> <dbl>
##  1 Morocco            Sardina pilchardus  1994   947
##  2 Morocco            Sardina pilchardus  1996   925
##  3 Spain              Sardina pilchardus  1996   912
##  4 Morocco            Sardina pilchardus  2000   859
##  5 Morocco            Sardina pilchardus  1990   845
##  6 Morocco            Sardina pilchardus  1991   827
##  7 Morocco            Sardina pilchardus  1998   723
##  8 Morocco            Sardina pilchardus  1993   710
##  9 Russian Federation Sardina pilchardus  1992   627
## 10 Russian Federation Sardina pilchardus  1991   579
## # ℹ 326 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, year, catch) %>% 
  filter(year>=2008 & year<=2012) %>% 
  filter(isscaap_taxonomic_group=="Squids, cuttlefishes, octopuses") %>% 
  arrange(desc(catch))
```

```
## # A tibble: 1,801 × 4
##    country                  isscaap_taxonomic_group          year catch
##    <chr>                    <chr>                           <dbl> <dbl>
##  1 Indonesia                Squids, cuttlefishes, octopuses  2012   991
##  2 China                    Squids, cuttlefishes, octopuses  2008   981
##  3 Chile                    Squids, cuttlefishes, octopuses  2012   965
##  4 United States of America Squids, cuttlefishes, octopuses  2010   901
##  5 China                    Squids, cuttlefishes, octopuses  2012   845
##  6 Japan                    Squids, cuttlefishes, octopuses  2010   832
##  7 China                    Squids, cuttlefishes, octopuses  2010   826
##  8 Peru                     Squids, cuttlefishes, octopuses  2010   822
##  9 Korea, Republic of       Squids, cuttlefishes, octopuses  2008   816
## 10 Peru                     Squids, cuttlefishes, octopuses  2009   805
## # ℹ 1,791 more rows
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_tidy %>% 
  select(asfis_species_name, year, catch) %>% 
  filter(year>=2008 & year<=2012) %>% 
  filter(asfis_species_name!="Osteichthyes") %>% 
  arrange(desc(catch))
```

```
## # A tibble: 49,554 × 3
##    asfis_species_name     year catch
##    <chr>                 <dbl> <dbl>
##  1 Trichiurus lepturus    2011  8221
##  2 Theragra chalcogramma  2012  8188
##  3 Engraulis ringens      2008  7981
##  4 Clupea harengus        2008  7873
##  5 Clupea harengus        2009  7250
##  6 Engraulis ringens      2012  6880
##  7 Trichiurus lepturus    2010  6841
##  8 Engraulis ringens      2008  6748
##  9 Trichiurus lepturus    2012  6694
## 10 Theragra chalcogramma  2009  6532
## # ℹ 49,544 more rows
```

10. Use the data to do at least one analysis of your choice.

```r
fisheries_tidy %>% 
  group_by(common_name) %>% 
  summarize(mean_catch=mean(catch, na.rm=T),
            min_catch=min(catch, na.rm=T),
            max_catch=max(catch, na.rm=T),
            total=n())
```

```
## Warning: There were 120 warnings in `summarize()`.
## The first warning was:
## ℹ In argument: `min_catch = min(catch, na.rm = T)`.
## ℹ In group 41: `common_name = "Antarctic armless flounder"`.
## Caused by warning in `min()`:
## ! no non-missing arguments to min; returning Inf
## ℹ Run `dplyr::last_dplyr_warnings()` to see the 119 remaining warnings.
```

```
## # A tibble: 1,551 × 5
##    common_name                    mean_catch min_catch max_catch total
##    <chr>                               <dbl>     <dbl>     <dbl> <int>
##  1 Abalones nei                        19.8          0        97   405
##  2 Acoupa weakfish                     44.8          2        79    11
##  3 Aesop shrimp                        38            1        89    11
##  4 African forktail snapper            12.1          1        50     9
##  5 African moonfish                    27.0          0        98   251
##  6 African sicklefish                  30.8          0        99   535
##  7 African striped grunt               84           84        84     2
##  8 Akiami paste shrimp                122.           0       966   148
##  9 Alaska plaice                        9.55         0        91    32
## 10 Alaska pollock(=Walleye poll.)    1084.           0      9928   469
## # ℹ 1,541 more rows
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
