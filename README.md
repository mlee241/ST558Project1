ST 558 Project 1
================
Marcus Lee
6/13/2021

-   [JSON Data](#json-data)
-   [Packages used for reading JSON data in
    R](#packages-used-for-reading-json-data-in-r)
-   [Contact the NHL Records API](#contact-the-nhl-records-api)
-   [Contact the NHL Stats API](#contact-the-nhl-stats-api)
    -   [More functions](#more-functions)
    -   [Wrapper functions](#wrapper-functions)
-   [Exploratory Data Analysis](#exploratory-data-analysis)

``` r
library(ggplot2)
library(jsonlite)
library(knitr)
library(httr)
```

# JSON Data

# Packages used for reading JSON data in R

# Contact the NHL Records API

``` r
base_url = "https://records.nhl.com/site/api"
```

``` r
get_franchise = function(){
  full_url = paste0(base_url, "/franchise")
  franchise_text = content(GET(url=full_url), "text")
  franchise_json = fromJSON(franchise_text, flatten = T)
  return(franchise_json$data)
}
```

``` r
get_franchise_team_totals = function(){
  full_url = paste0(base_url, "/franchise-team-totals")
  franchise_team_totals_text = content(GET(url=full_url), "text")
  franchise_team_totals_json = fromJSON(franchise_team_totals_text, flatten = T)
  return(franchise_team_totals_json$data)
}
```

``` r
get_franchise_season_records = function(id){
  full_url = paste0(base_url, "/franchise-season-records?cayenneExp=franchiseId=",id)
  franchise_season_records_text = content(GET(url=full_url), "text")
  franchise_season_records_json = fromJSON(franchise_season_records_text, flatten = T)
  return(franchise_season_records_json$data)
}
```

``` r
get_franchise_goalie_records = function(id){
  full_url = paste0(base_url, "/franchise-goalie-records?cayenneExp=franchiseId=",id)
  franchise_goalie_records_text = content(GET(url=full_url), "text")
  franchise_goalie_records_json = fromJSON(franchise_goalie_records_text, flatten = T)
  return(franchise_goalie_records_json$data)
}
```

``` r
get_franchise_skater_records = function(id){
  full_url = paste0(base_url, "/franchise-skater-records?cayenneExp=franchiseId=",id)
  franchise_skater_records_text = content(GET(url=full_url), "text")
  franchise_skater_records_json = fromJSON(franchise_skater_records_text, flatten = T)
  return(franchise_skater_records_json$data)
}
```

``` r
get_franchise_detail = function(id){
  full_url = paste0(base_url, "/franchise-detail?cayenneExp=mostRecentTeamId=",id)
  franchise_detail_text = content(GET(url=full_url), "text")
  franchise_detail_json = fromJSON(franchise_detail_text, flatten = T)
  return(franchise_detail_json$data)
}
```

``` r
kable(franchise)
```

|  id | firstSeasonId | fullName              | lastSeasonId | mostRecentTeamId | teamAbbrev | teamCommonName | teamPlaceName |
|----:|--------------:|:----------------------|-------------:|-----------------:|:-----------|:---------------|:--------------|
|   1 |      19171918 | Montréal Canadiens    |           NA |                8 | MTL        | Canadiens      | Montréal      |
|   2 |      19171918 | Montreal Wanderers    |     19171918 |               41 | MWN        | Wanderers      | Montreal      |
|   3 |      19171918 | St. Louis Eagles      |     19341935 |               45 | SLE        | Eagles         | St. Louis     |
|   4 |      19191920 | Hamilton Tigers       |     19241925 |               37 | HAM        | Tigers         | Hamilton      |
|   5 |      19171918 | Toronto Maple Leafs   |           NA |               10 | TOR        | Maple Leafs    | Toronto       |
|   6 |      19241925 | Boston Bruins         |           NA |                6 | BOS        | Bruins         | Boston        |
|   7 |      19241925 | Montreal Maroons      |     19371938 |               43 | MMR        | Maroons        | Montreal      |
|   8 |      19251926 | Brooklyn Americans    |     19411942 |               51 | BRK        | Americans      | Brooklyn      |
|   9 |      19251926 | Philadelphia Quakers  |     19301931 |               39 | QUA        | Quakers        | Philadelphia  |
|  10 |      19261927 | New York Rangers      |           NA |                3 | NYR        | Rangers        | New York      |
|  11 |      19261927 | Chicago Blackhawks    |           NA |               16 | CHI        | Blackhawks     | Chicago       |
|  12 |      19261927 | Detroit Red Wings     |           NA |               17 | DET        | Red Wings      | Detroit       |
|  13 |      19671968 | Cleveland Barons      |     19771978 |               49 | CLE        | Barons         | Cleveland     |
|  14 |      19671968 | Los Angeles Kings     |           NA |               26 | LAK        | Kings          | Los Angeles   |
|  15 |      19671968 | Dallas Stars          |           NA |               25 | DAL        | Stars          | Dallas        |
|  16 |      19671968 | Philadelphia Flyers   |           NA |                4 | PHI        | Flyers         | Philadelphia  |
|  17 |      19671968 | Pittsburgh Penguins   |           NA |                5 | PIT        | Penguins       | Pittsburgh    |
|  18 |      19671968 | St. Louis Blues       |           NA |               19 | STL        | Blues          | St. Louis     |
|  19 |      19701971 | Buffalo Sabres        |           NA |                7 | BUF        | Sabres         | Buffalo       |
|  20 |      19701971 | Vancouver Canucks     |           NA |               23 | VAN        | Canucks        | Vancouver     |
|  21 |      19721973 | Calgary Flames        |           NA |               20 | CGY        | Flames         | Calgary       |
|  22 |      19721973 | New York Islanders    |           NA |                2 | NYI        | Islanders      | New York      |
|  23 |      19741975 | New Jersey Devils     |           NA |                1 | NJD        | Devils         | New Jersey    |
|  24 |      19741975 | Washington Capitals   |           NA |               15 | WSH        | Capitals       | Washington    |
|  25 |      19791980 | Edmonton Oilers       |           NA |               22 | EDM        | Oilers         | Edmonton      |
|  26 |      19791980 | Carolina Hurricanes   |           NA |               12 | CAR        | Hurricanes     | Carolina      |
|  27 |      19791980 | Colorado Avalanche    |           NA |               21 | COL        | Avalanche      | Colorado      |
|  28 |      19791980 | Arizona Coyotes       |           NA |               53 | ARI        | Coyotes        | Arizona       |
|  29 |      19911992 | San Jose Sharks       |           NA |               28 | SJS        | Sharks         | San Jose      |
|  30 |      19921993 | Ottawa Senators       |           NA |                9 | OTT        | Senators       | Ottawa        |
|  31 |      19921993 | Tampa Bay Lightning   |           NA |               14 | TBL        | Lightning      | Tampa Bay     |
|  32 |      19931994 | Anaheim Ducks         |           NA |               24 | ANA        | Ducks          | Anaheim       |
|  33 |      19931994 | Florida Panthers      |           NA |               13 | FLA        | Panthers       | Florida       |
|  34 |      19981999 | Nashville Predators   |           NA |               18 | NSH        | Predators      | Nashville     |
|  35 |      19992000 | Winnipeg Jets         |           NA |               52 | WPG        | Jets           | Winnipeg      |
|  36 |      20002001 | Columbus Blue Jackets |           NA |               29 | CBJ        | Blue Jackets   | Columbus      |
|  37 |      20002001 | Minnesota Wild        |           NA |               30 | MIN        | Wild           | Minnesota     |
|  38 |      20172018 | Vegas Golden Knights  |           NA |               54 | VGK        | Golden Knights | Vegas         |
|  39 |      20212022 | Seattle Kraken        |           NA |               55 | SEA        | Kraken         | Seattle       |

# Contact the NHL Stats API

``` r
base_stats_url = "https://statsapi.web.nhl.com/api/v1"
```

``` r
get_team_stats = function(id){
  if (missing(id)==T){
    full_url = paste0(base_stats_url, "/teams?expand=team.stats=")
    team.stats_text = content(GET(url=full_url), "text")
    team.stats_json = fromJSON(team.stats_text, flatten = T)
    team.stats2none_json = team.stats_json[2] # We are ignoring the 1st list since it it useless
    return(team.stats2none_json)
  }
  else{
    full_url =  paste0(base_stats_url, "/teams/",id)
    team.stats_text = content(GET(url=full_url), "text")
    team.stats_json = fromJSON(team.stats_text, flatten = T)
    team.stats2id_json = team.stats_json[2] # We are ignoring the 1st list since it it useless
    return(team.stats2id_json)
  }
  # if(...==TRUE){
  #   if(is.numeric(...)==FALSE){
  #     id=1
  #     full_url =  paste0(base_stats_url, "/teams/",id)
  #   }else{
  #     full_url =  paste0(base_stats_url, "/teams/",id)
  #   }
    #full_url =  paste0(base_stats_url, "/teams/",id)
  #}
  # T  - solved
  # F - solved
  # T, number- solved
  # F, number- solved
  # number, F
  # number , T
  # else{
  #   # This should return all of the data from all teams.
  #   full_url = paste0(base_stats_url, "/teams?expand=team.stats=")
  # }
  # team.stats_text = content(GET(url=full_url), "text")
  # team.stats_json = fromJSON(team.stats_text, flatten = T)
  # team.stats2_json = team.stats_json[2] # We are ignoring the 1st list since it it useless
  # #print(team.stats2_json)
  # return(team.stats2_json)
}
```

``` r
id=2
team.stats = get_team_stats(id)
```

``` r
kable(team.stats)
```

<table class="kable_wrapper">
<tbody>
<tr>
<td>

|  id | name               | link            | abbreviation | teamName  | locationName | firstYearOfPlay | shortName    | officialSiteUrl                    | franchiseId | active | venue.name                        | venue.link          | venue.city | venue.timeZone.id | venue.timeZone.offset | venue.timeZone.tz | division.id | division.name   | division.link        | conference.id | conference.name | conference.link       | franchise.franchiseId | franchise.teamName | franchise.link        |
|----:|:-------------------|:----------------|:-------------|:----------|:-------------|:----------------|:-------------|:-----------------------------------|------------:|:-------|:----------------------------------|:--------------------|:-----------|:------------------|----------------------:|:------------------|------------:|:----------------|:---------------------|--------------:|:----------------|:----------------------|----------------------:|:-------------------|:----------------------|
|   2 | New York Islanders | /api/v1/teams/2 | NYI          | Islanders | New York     | 1972            | NY Islanders | <http://www.newyorkislanders.com/> |          22 | TRUE   | Nassau Veterans Memorial Coliseum | /api/v1/venues/null | Uniondale  | America/New\_York |                    -4 | EDT               |          25 | MassMutual East | /api/v1/divisions/25 |             6 | Eastern         | /api/v1/conferences/6 |                    22 | Islanders          | /api/v1/franchises/22 |

</td>
</tr>
</tbody>
</table>

``` r
# So wrapper function could call for modifier(team.stats) or like individual id
#needs to get like the records api as well
#get_wrapper <- function(x, ){
#  return(get_team_stats(x,))
#}
```

``` r
# so users can enter team id or the modifere here
#wrap = get_wrapper(2,TRUE)
```

## More functions

## Wrapper functions

# Exploratory Data Analysis
