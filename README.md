JSON Data - A Vignette by Saara Raja
================

-   [JSON Data](#json-data)
-   [Reading JSON Data into R](#reading-json-data-into-r)
-   [Connect to NHL Data](#connect-to-nhl-data)

JSON Data
---------

Text to Go Here

Reading JSON Data into R
------------------------

Text to Go Here

Connect to NHL Data
-------------------

``` r
library(httr)
library(jsonlite)
library(tidyverse)
library(tidyjson)

base <- "https://records.nhl.com/site/api"
endpoint <- "/franchise"
call1 <- paste0(base, endpoint)

get_franchise <- GET(call1)
get_franchise_text <- content(get_franchise, "text")

get_franchise_text %>% gather_object %>% json_types %>% count(name, type)
```

    ## # A tibble: 2 x 3
    ##   name  type       n
    ##   <chr> <fct>  <int>
    ## 1 data  array      1
    ## 2 total number     1

``` r
franchise_prelim <- get_franchise_text %>%
  enter_object(data) %>%
  gather_array %>%
  spread_all

franchise <- as.tibble(franchise_prelim) 
```

    ## Warning: `as.tibble()` is deprecated as of tibble 2.0.0.
    ## Please use `as_tibble()` instead.
    ## The signature and semantics have changed, see `?as_tibble`.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_warnings()` to see where this warning was generated.

``` r
 franchise %>% select(id, firstSeasonId, lastSeasonId, teamCommonName)
```

    ## # A tibble: 38 x 4
    ##       id firstSeasonId lastSeasonId teamCommonName
    ##    <dbl>         <dbl>        <dbl> <chr>         
    ##  1     1      19171918           NA Canadiens     
    ##  2     2      19171918     19171918 Wanderers     
    ##  3     3      19171918     19341935 Eagles        
    ##  4     4      19191920     19241925 Tigers        
    ##  5     5      19171918           NA Maple Leafs   
    ##  6     6      19241925           NA Bruins        
    ##  7     7      19241925     19371938 Maroons       
    ##  8     8      19251926     19411942 Americans     
    ##  9     9      19251926     19301931 Quakers       
    ## 10    10      19261927           NA Rangers       
    ## # … with 28 more rows

``` r
#get_franchise_json <- fromJSON(get_franchise_text, flatten = TRUE, simplifyDataFrame = TRUE)
#get_franchise_df <- as_tibble(get_franchise_json)

#names(get_franchise_df)
#get_franchise_df
#franchise <- get_franchise_df %>% select("$id", "$firstSeasonId", "$lastSeasonId", "$teamCommonName")

#print(franchise)
```
