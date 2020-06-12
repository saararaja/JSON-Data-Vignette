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
base <- "https://records.nhl.com/site/api"

franch_func <- function(){
  
  #url ending
  endpoint <- "/franchise"
  #Create the url & read in the data 
  call1 <- paste0(base, endpoint)
  get_franchise <- GET(call1)
  get_franchise_text <- content(get_franchise, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  franchise_prelim <- get_franchise_text %>% enter_object(data) %>%
                      gather_array %>% spread_all
  
  franchise <- as_tibble(franchise_prelim) 
  
  franchise <- franchise %>% select(id, firstSeasonId, lastSeasonId, teamCommonName)
  
  return(franchise)
}
```

``` r
franchise <- franch_func() 
franchise
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
