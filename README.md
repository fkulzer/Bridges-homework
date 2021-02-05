Bridges homework
================
Faith Kulzer
2/4/2021

``` r
library('readr')
library('data.table')
library('tidyverse')
```

    ## -- Attaching packages ------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v dplyr   1.0.2
    ## v tibble  3.0.3     v stringr 1.4.0
    ## v tidyr   1.1.2     v forcats 0.5.0
    ## v purrr   0.3.4

    ## -- Conflicts ---------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::between()   masks data.table::between()
    ## x dplyr::filter()    masks stats::filter()
    ## x dplyr::first()     masks data.table::first()
    ## x dplyr::lag()       masks stats::lag()
    ## x dplyr::last()      masks data.table::last()
    ## x purrr::transpose() masks data.table::transpose()

``` r
bridges <- fread("2019HwyBridgesDelimitedAllStates.txt")


##filter out useful columns, rename
bridges_filtered <- bridges %>%
  select(STRUCTURE_NUMBER_008, COUNTY_CODE_003, DECK_COND_058, SUPERSTRUCTURE_COND_059, SUBSTRUCTURE_COND_060, YEAR_BUILT_027, ADT_029, LAT_016, LONG_017) %>%
  rename(bridge_id = STRUCTURE_NUMBER_008, fip_code = COUNTY_CODE_003, deck_cond = DECK_COND_058, super_cond = SUPERSTRUCTURE_COND_059, sub_cond = SUBSTRUCTURE_COND_060, year = YEAR_BUILT_027, adt = ADT_029, latitude = LAT_016, longitude = LONG_017)

head(bridges_filtered)
```

    ##          bridge_id fip_code deck_cond super_cond sub_cond year  adt latitude
    ## 1: 00000000000S702       53         8          8        7 1999   50 31061094
    ## 2: 00000000000S703       53         8          8        7 2002  159 31062020
    ## 3: 0000000000M0022      113         5          5        6 1942  375 32174330
    ## 4: 000000883039900       59         7          7        7 1974  430 34270600
    ## 5: 000001014002450       79         5          6        5 1937 5520 34481800
    ## 6: 000001331700710       33         5          5        5 1924 3620 34480000
    ##    longitude
    ## 1:  87341348
    ## 2:  87340890
    ## 3:  84583799
    ## 4:  87581200
    ## 5:  87225400
    ## 6:  87373000

``` r
ggplot(bridges_filtered, aes(x=longitude, y=adt)) +
  geom_point(size=0.4) +
  xlab("Longitude") +
  ylab("Average Daily Travel") +
  geom_vline(xintercept = 93265000, color="red")
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

This graph shows the average daily travel for each bridge by the
longitude coordinate of the bridge. Shown for context is the longitude
of Minneapolis, Minnesota, indicated by the red vertical line. At this
longitude I would guess that many bridges are made crossing the
Mississippi River.
