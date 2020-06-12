JSON Data - A Vignette by Saara Raja
================

-   [JSON Data Overview](#json-data-overview)
    -   [Data Structure](#data-structure)
-   [Reading JSON Data into R](#reading-json-data-into-r)
-   [Connect to NHL Data](#connect-to-nhl-data)

JSON Data Overview
------------------

**JSON**, or Java Script Object Notation, Data is a purely text-based way of storing data and is the primary way of data storage/retrieval of web information. Because of its simplistic text format, JSON data is easy to read and understand by humans, while also enabling easy data parsing by a computer, hence its popularity. XML, an alternative text-based data interchange method, has a much more complex/verbose syntax and is more challenging for humans to code and understand, causing JSON to eclipse it as the most popular method of exchanging web information. JSON is the most popular method of extracting data from REST APIs, so having a good understanding of the format is valuable for any analytics on web-based data.

### Data Structure

The JSON data structure is in the form of nested key-value pairs and ordered lists. The following image shows the general format of JSON data. The original image along with more information can be found [here](https://www.goanywhere.com/managed-file-transfer/more/tutorials/parse-json-data-into-database).

<img src="ExampleJSON2.png" width="60%" />

As we can see from the image, JSON objects are created within `{}` curly brackets and each variable is paired with its value is `"key":"value"` format. All values are placed within double quotes, whether they are of character or numeric type. Data can also have multiple values that is depicted using `[]` square brackets to show arrays. Arrays are an ordered list of key-value pairs, separated by commas.

In this particular image, there is a JSON object called "orders" which has several attributes ("orderno", "date", "trackingno", etc) that are displayed as nested key-value pairs in an array . This nested format shows that each of these variables is related to the original parent variable "orders". In addition, the variable "customer" has further attributes of its own, which are displayed in a 3rd layer nested key-value pairs in an array.

Further information on JSON data can be found [here](https://www.infoworld.com/article/3222851/what-is-json-a-better-format-for-data-exchange.html).

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
  get_json <- GET(call1)
  get_json_text <- content(get_json, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  df_prelim <- get_json_text %>% enter_object(data) %>% gather_array %>% spread_all
  df <- as_tibble(df_prelim) 
  df <- df %>% select(-document.id, -array.index)
  return(df)
}
```

``` r
franchise <- franch_func() 
franchise
```

    ## # A tibble: 38 x 6
    ##       id firstSeasonId lastSeasonId mostRecentTeamId teamCommonName
    ##    <dbl>         <dbl>        <dbl>            <dbl> <chr>         
    ##  1     1      19171918           NA                8 Canadiens     
    ##  2     2      19171918     19171918               41 Wanderers     
    ##  3     3      19171918     19341935               45 Eagles        
    ##  4     4      19191920     19241925               37 Tigers        
    ##  5     5      19171918           NA               10 Maple Leafs   
    ##  6     6      19241925           NA                6 Bruins        
    ##  7     7      19241925     19371938               43 Maroons       
    ##  8     8      19251926     19411942               51 Americans     
    ##  9     9      19251926     19301931               39 Quakers       
    ## 10    10      19261927           NA                3 Rangers       
    ## # … with 28 more rows, and 1 more variable: teamPlaceName <chr>

``` r
franch_total_func <- function(){
  
  #url ending
  endpoint <- "/franchise-team-totals"
  
  #Create the url & read in the data 
  call1 <- paste0(base, endpoint)
  get_json <- GET(call1)
  get_json_text <- content(get_json, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  df_prelim <- get_json_text %>% enter_object(data) %>% gather_array %>% spread_all
  df <- as_tibble(df_prelim) 
  df <- df %>% select(-document.id, -array.index)
  return(df)
}
```

``` r
franch_total <- franch_total_func()
franch_total
```

    ## # A tibble: 104 x 30
    ##       id activeFranchise firstSeasonId franchiseId gameTypeId gamesPlayed
    ##    <dbl>           <dbl>         <dbl>       <dbl>      <dbl>       <dbl>
    ##  1     1               1      19821983          23          2        2937
    ##  2     2               1      19821983          23          3         257
    ##  3     3               1      19721973          22          2        3732
    ##  4     4               1      19721973          22          3         272
    ##  5     5               1      19261927          10          2        6504
    ##  6     6               1      19261927          10          3         515
    ##  7     7               1      19671968          16          3         433
    ##  8     8               1      19671968          16          2        4115
    ##  9     9               1      19671968          17          2        4115
    ## 10    10               1      19671968          17          3         381
    ## # … with 94 more rows, and 24 more variables: goalsAgainst <dbl>,
    ## #   goalsFor <dbl>, homeLosses <dbl>, homeOvertimeLosses <dbl>, homeTies <dbl>,
    ## #   homeWins <dbl>, lastSeasonId <dbl>, losses <dbl>, overtimeLosses <dbl>,
    ## #   penaltyMinutes <dbl>, pointPctg <dbl>, points <dbl>, roadLosses <dbl>,
    ## #   roadOvertimeLosses <dbl>, roadTies <dbl>, roadWins <dbl>,
    ## #   shootoutLosses <dbl>, shootoutWins <dbl>, shutouts <dbl>, teamId <dbl>,
    ## #   teamName <chr>, ties <dbl>, triCode <chr>, wins <dbl>

``` r
franch_season_func <- function(number){
  
  #url ending
  endpoint <- "/franchise-season-records?cayenneExp=franchiseId="
  
  #Create the url & read in the data 
  call1 <- paste0(base, endpoint, number)
  get_json <- GET(call1)
  get_json_text <- content(get_json, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  df_prelim <- get_json_text %>% enter_object(data) %>% gather_array %>% spread_all
  df <- as_tibble(df_prelim) 
  df <- df %>% select(-document.id, -array.index)
  return(df)
}
```

``` r
franch_season <- franch_season_func(3)
franch_season
```

    ## # A tibble: 1 x 57
    ##      id fewestGoals fewestGoalsAgai… fewestGoalsAgai… fewestGoalsSeas…
    ##   <dbl> <lgl>       <lgl>            <lgl>            <lgl>           
    ## 1    36 NA          NA               NA               NA              
    ## # … with 52 more variables: fewestLosses <lgl>, fewestLossesSeasons <lgl>,
    ## #   fewestPoints <lgl>, fewestPointsSeasons <lgl>, fewestTies <lgl>,
    ## #   fewestTiesSeasons <lgl>, fewestWins <lgl>, fewestWinsSeasons <lgl>,
    ## #   franchiseId <dbl>, franchiseName <chr>, homeLossStreak <dbl>,
    ## #   homeLossStreakDates <chr>, homePointStreak <dbl>,
    ## #   homePointStreakDates <chr>, homeWinStreak <dbl>, homeWinStreakDates <chr>,
    ## #   homeWinlessStreak <dbl>, homeWinlessStreakDates <chr>, lossStreak <dbl>,
    ## #   lossStreakDates <chr>, mostGameGoals <dbl>, mostGameGoalsDates <chr>,
    ## #   mostGoals <dbl>, mostGoalsAgainst <dbl>, mostGoalsAgainstSeasons <chr>,
    ## #   mostGoalsSeasons <chr>, mostLosses <dbl>, mostLossesSeasons <chr>,
    ## #   mostPenaltyMinutes <dbl>, mostPenaltyMinutesSeasons <chr>,
    ## #   mostPoints <dbl>, mostPointsSeasons <chr>, mostShutouts <dbl>,
    ## #   mostShutoutsSeasons <chr>, mostTies <dbl>, mostTiesSeasons <chr>,
    ## #   mostWins <dbl>, mostWinsSeasons <chr>, pointStreak <dbl>,
    ## #   pointStreakDates <chr>, roadLossStreak <dbl>, roadLossStreakDates <chr>,
    ## #   roadPointStreak <dbl>, roadPointStreakDates <chr>, roadWinStreak <dbl>,
    ## #   roadWinStreakDates <chr>, roadWinlessStreak <dbl>,
    ## #   roadWinlessStreakDates <chr>, winStreak <dbl>, winStreakDates <chr>,
    ## #   winlessStreak <lgl>, winlessStreakDates <lgl>

``` r
franch_goalie_func <- function(number){
  
  #url ending
  endpoint <- "/franchise-goalie-records?cayenneExp=franchiseId="
  
  #Create the url & read in the data 
  call1 <- paste0(base, endpoint, number)
  get_json <- GET(call1)
  get_json_text <- content(get_json, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  df_prelim <- get_json_text %>% enter_object(data) %>% gather_array %>% spread_all
  df <- as_tibble(df_prelim) 
  df <- df %>% select(-document.id, -array.index)
  return(df)
}
```

``` r
franch_goalie <- franch_goalie_func(3)
franch_goalie
```

    ## # A tibble: 4 x 29
    ##      id activePlayer firstName franchiseId franchiseName gameTypeId gamesPlayed
    ##   <dbl> <lgl>        <chr>           <dbl> <chr>              <dbl>       <dbl>
    ## 1   248 FALSE        Alec                3 St. Louis Ea…          2         294
    ## 2   538 FALSE        Bill                3 St. Louis Ea…          2          90
    ## 3   600 FALSE        Sammy               3 St. Louis Ea…          2           2
    ## 4  1231 FALSE        Clint               3 St. Louis Ea…          2         158
    ## # … with 22 more variables: lastName <chr>, losses <dbl>,
    ## #   mostGoalsAgainstDates <chr>, mostGoalsAgainstOneGame <dbl>,
    ## #   mostSavesDates <lgl>, mostSavesOneGame <lgl>, mostShotsAgainstDates <lgl>,
    ## #   mostShotsAgainstOneGame <lgl>, mostShutoutsOneSeason <dbl>,
    ## #   mostShutoutsSeasonIds <chr>, mostWinsOneSeason <dbl>,
    ## #   mostWinsSeasonIds <chr>, overtimeLosses <lgl>, playerId <dbl>,
    ## #   positionCode <chr>, rookieGamesPlayed <dbl>, rookieShutouts <dbl>,
    ## #   rookieWins <dbl>, seasons <dbl>, shutouts <dbl>, ties <dbl>, wins <dbl>

``` r
franch_skater_func <- function(number){
  
  #url ending
  endpoint <- "/franchise-skater-records?cayenneExp=franchiseId="
  
  #Create the url & read in the data 
  call1 <- paste0(base, endpoint, number)
  get_json <- GET(call1)
  get_json_text <- content(get_json, "text")
  
  #use tidyjson to convert the data into a useable dataframe
  df_prelim <- get_json_text %>% enter_object(data) %>% gather_array %>% spread_all
  df <- as_tibble(df_prelim) 
  df <- df %>% select(-document.id, -array.index)
  return(df)
}
```

``` r
franch_skater <- franch_skater_func(3)
franch_skater
```

    ## # A tibble: 90 x 30
    ##       id activePlayer assists firstName franchiseId franchiseName gameTypeId
    ##    <dbl> <lgl>          <dbl> <chr>           <dbl> <chr>              <dbl>
    ##  1 16907 FALSE            100 Frank               3 St. Louis Ea…          2
    ##  2 16979 FALSE             67 Frank               3 St. Louis Ea…          2
    ##  3 16985 FALSE             87 Cy                  3 St. Louis Ea…          2
    ##  4 17012 FALSE             75 George              3 St. Louis Ea…          2
    ##  5 17047 FALSE             57 Hec                 3 St. Louis Ea…          2
    ##  6 17067 FALSE             72 King                3 St. Louis Ea…          2
    ##  7 17104 FALSE             29 Hooley              3 St. Louis Ea…          2
    ##  8 17150 FALSE             46 Joe                 3 St. Louis Ea…          2
    ##  9 17209 FALSE              1 Jack                3 St. Louis Ea…          2
    ## 10 17352 FALSE              7 Ossie               3 St. Louis Ea…          2
    ## # … with 80 more rows, and 23 more variables: gamesPlayed <dbl>, goals <dbl>,
    ## #   lastName <chr>, mostAssistsGameDates <chr>, mostAssistsOneGame <dbl>,
    ## #   mostAssistsOneSeason <dbl>, mostAssistsSeasonIds <chr>,
    ## #   mostGoalsGameDates <chr>, mostGoalsOneGame <dbl>, mostGoalsOneSeason <dbl>,
    ## #   mostGoalsSeasonIds <chr>, mostPenaltyMinutesOneSeason <dbl>,
    ## #   mostPenaltyMinutesSeasonIds <chr>, mostPointsGameDates <chr>,
    ## #   mostPointsOneGame <dbl>, mostPointsOneSeason <dbl>,
    ## #   mostPointsSeasonIds <chr>, penaltyMinutes <dbl>, playerId <dbl>,
    ## #   points <dbl>, positionCode <chr>, rookiePoints <dbl>, seasons <dbl>
