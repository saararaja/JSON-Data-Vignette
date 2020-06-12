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

base <- "https://records.nhl.com/site/api"
endpoint <- "/franchise"
call1 <- paste0(base, endpoint)

get_franchise <- GET(call1)
get_franchise_text <- content(get_franchise, "text")

get_franchise_text
```

    ## [1] "{\"data\":[{\"id\":1,\"firstSeasonId\":19171918,\"lastSeasonId\":null,\"mostRecentTeamId\":8,\"teamCommonName\":\"Canadiens\",\"teamPlaceName\":\"Montréal\"},{\"id\":2,\"firstSeasonId\":19171918,\"lastSeasonId\":19171918,\"mostRecentTeamId\":41,\"teamCommonName\":\"Wanderers\",\"teamPlaceName\":\"Montreal\"},{\"id\":3,\"firstSeasonId\":19171918,\"lastSeasonId\":19341935,\"mostRecentTeamId\":45,\"teamCommonName\":\"Eagles\",\"teamPlaceName\":\"St. Louis\"},{\"id\":4,\"firstSeasonId\":19191920,\"lastSeasonId\":19241925,\"mostRecentTeamId\":37,\"teamCommonName\":\"Tigers\",\"teamPlaceName\":\"Hamilton\"},{\"id\":5,\"firstSeasonId\":19171918,\"lastSeasonId\":null,\"mostRecentTeamId\":10,\"teamCommonName\":\"Maple Leafs\",\"teamPlaceName\":\"Toronto\"},{\"id\":6,\"firstSeasonId\":19241925,\"lastSeasonId\":null,\"mostRecentTeamId\":6,\"teamCommonName\":\"Bruins\",\"teamPlaceName\":\"Boston\"},{\"id\":7,\"firstSeasonId\":19241925,\"lastSeasonId\":19371938,\"mostRecentTeamId\":43,\"teamCommonName\":\"Maroons\",\"teamPlaceName\":\"Montreal\"},{\"id\":8,\"firstSeasonId\":19251926,\"lastSeasonId\":19411942,\"mostRecentTeamId\":51,\"teamCommonName\":\"Americans\",\"teamPlaceName\":\"Brooklyn\"},{\"id\":9,\"firstSeasonId\":19251926,\"lastSeasonId\":19301931,\"mostRecentTeamId\":39,\"teamCommonName\":\"Quakers\",\"teamPlaceName\":\"Philadelphia\"},{\"id\":10,\"firstSeasonId\":19261927,\"lastSeasonId\":null,\"mostRecentTeamId\":3,\"teamCommonName\":\"Rangers\",\"teamPlaceName\":\"New York\"},{\"id\":11,\"firstSeasonId\":19261927,\"lastSeasonId\":null,\"mostRecentTeamId\":16,\"teamCommonName\":\"Blackhawks\",\"teamPlaceName\":\"Chicago\"},{\"id\":12,\"firstSeasonId\":19261927,\"lastSeasonId\":null,\"mostRecentTeamId\":17,\"teamCommonName\":\"Red Wings\",\"teamPlaceName\":\"Detroit\"},{\"id\":13,\"firstSeasonId\":19671968,\"lastSeasonId\":19771978,\"mostRecentTeamId\":49,\"teamCommonName\":\"Barons\",\"teamPlaceName\":\"Cleveland\"},{\"id\":14,\"firstSeasonId\":19671968,\"lastSeasonId\":null,\"mostRecentTeamId\":26,\"teamCommonName\":\"Kings\",\"teamPlaceName\":\"Los Angeles\"},{\"id\":15,\"firstSeasonId\":19671968,\"lastSeasonId\":null,\"mostRecentTeamId\":25,\"teamCommonName\":\"Stars\",\"teamPlaceName\":\"Dallas\"},{\"id\":16,\"firstSeasonId\":19671968,\"lastSeasonId\":null,\"mostRecentTeamId\":4,\"teamCommonName\":\"Flyers\",\"teamPlaceName\":\"Philadelphia\"},{\"id\":17,\"firstSeasonId\":19671968,\"lastSeasonId\":null,\"mostRecentTeamId\":5,\"teamCommonName\":\"Penguins\",\"teamPlaceName\":\"Pittsburgh\"},{\"id\":18,\"firstSeasonId\":19671968,\"lastSeasonId\":null,\"mostRecentTeamId\":19,\"teamCommonName\":\"Blues\",\"teamPlaceName\":\"St. Louis\"},{\"id\":19,\"firstSeasonId\":19701971,\"lastSeasonId\":null,\"mostRecentTeamId\":7,\"teamCommonName\":\"Sabres\",\"teamPlaceName\":\"Buffalo\"},{\"id\":20,\"firstSeasonId\":19701971,\"lastSeasonId\":null,\"mostRecentTeamId\":23,\"teamCommonName\":\"Canucks\",\"teamPlaceName\":\"Vancouver\"},{\"id\":21,\"firstSeasonId\":19721973,\"lastSeasonId\":null,\"mostRecentTeamId\":20,\"teamCommonName\":\"Flames\",\"teamPlaceName\":\"Calgary\"},{\"id\":22,\"firstSeasonId\":19721973,\"lastSeasonId\":null,\"mostRecentTeamId\":2,\"teamCommonName\":\"Islanders\",\"teamPlaceName\":\"New York\"},{\"id\":23,\"firstSeasonId\":19741975,\"lastSeasonId\":null,\"mostRecentTeamId\":1,\"teamCommonName\":\"Devils\",\"teamPlaceName\":\"New Jersey\"},{\"id\":24,\"firstSeasonId\":19741975,\"lastSeasonId\":null,\"mostRecentTeamId\":15,\"teamCommonName\":\"Capitals\",\"teamPlaceName\":\"Washington\"},{\"id\":25,\"firstSeasonId\":19791980,\"lastSeasonId\":null,\"mostRecentTeamId\":22,\"teamCommonName\":\"Oilers\",\"teamPlaceName\":\"Edmonton\"},{\"id\":26,\"firstSeasonId\":19791980,\"lastSeasonId\":null,\"mostRecentTeamId\":12,\"teamCommonName\":\"Hurricanes\",\"teamPlaceName\":\"Carolina\"},{\"id\":27,\"firstSeasonId\":19791980,\"lastSeasonId\":null,\"mostRecentTeamId\":21,\"teamCommonName\":\"Avalanche\",\"teamPlaceName\":\"Colorado\"},{\"id\":28,\"firstSeasonId\":19791980,\"lastSeasonId\":null,\"mostRecentTeamId\":53,\"teamCommonName\":\"Coyotes\",\"teamPlaceName\":\"Arizona\"},{\"id\":29,\"firstSeasonId\":19911992,\"lastSeasonId\":null,\"mostRecentTeamId\":28,\"teamCommonName\":\"Sharks\",\"teamPlaceName\":\"San Jose\"},{\"id\":30,\"firstSeasonId\":19921993,\"lastSeasonId\":null,\"mostRecentTeamId\":9,\"teamCommonName\":\"Senators\",\"teamPlaceName\":\"Ottawa\"},{\"id\":31,\"firstSeasonId\":19921993,\"lastSeasonId\":null,\"mostRecentTeamId\":14,\"teamCommonName\":\"Lightning\",\"teamPlaceName\":\"Tampa Bay\"},{\"id\":32,\"firstSeasonId\":19931994,\"lastSeasonId\":null,\"mostRecentTeamId\":24,\"teamCommonName\":\"Ducks\",\"teamPlaceName\":\"Anaheim\"},{\"id\":33,\"firstSeasonId\":19931994,\"lastSeasonId\":null,\"mostRecentTeamId\":13,\"teamCommonName\":\"Panthers\",\"teamPlaceName\":\"Florida\"},{\"id\":34,\"firstSeasonId\":19981999,\"lastSeasonId\":null,\"mostRecentTeamId\":18,\"teamCommonName\":\"Predators\",\"teamPlaceName\":\"Nashville\"},{\"id\":35,\"firstSeasonId\":19992000,\"lastSeasonId\":null,\"mostRecentTeamId\":52,\"teamCommonName\":\"Jets\",\"teamPlaceName\":\"Winnipeg\"},{\"id\":36,\"firstSeasonId\":20002001,\"lastSeasonId\":null,\"mostRecentTeamId\":29,\"teamCommonName\":\"Blue Jackets\",\"teamPlaceName\":\"Columbus\"},{\"id\":37,\"firstSeasonId\":20002001,\"lastSeasonId\":null,\"mostRecentTeamId\":30,\"teamCommonName\":\"Wild\",\"teamPlaceName\":\"Minnesota\"},{\"id\":38,\"firstSeasonId\":20172018,\"lastSeasonId\":null,\"mostRecentTeamId\":54,\"teamCommonName\":\"Golden Knights\",\"teamPlaceName\":\"Vegas\"}],\"total\":38}"
