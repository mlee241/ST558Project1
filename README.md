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
#https://statsapi.web.nhl.com/api/v1/expands
```

``` r
get_team_stats = function(){
  # Not sure if I am doing this correctly
  #?stats=statsSingleSeasonPlayoffs
  #?expand=team.stats
  full_url = paste0(base_stats_url, "/teams?expand=team.stats=")
  team.stats_text = content(GET(url=full_url), "text")
  team.stats_json = fromJSON(team.stats_text, flatten = T)
  #team.stats2 <- team.stats[2]
  #return(team.stats2)
  #return(team.stats_json$data)#This is giving me a null answer
  return(team.stats_json)
  #return(team.stats_df)
}
```

``` r
#id=2
team.stats = get_team_stats()
```

``` r
# We are ignoring team.stats[1]
team.stats2 <- team.stats[2]
```

``` r
kable(team.stats2)
```

<table class="kable_wrapper">
<tbody>
<tr>
<td>

|  id | name                  | link             | abbreviation | teamName       | locationName | firstYearOfPlay | shortName    | officialSiteUrl                      | franchiseId | active | venue.name                        | venue.link          | venue.city   | venue.id | venue.timeZone.id    | venue.timeZone.offset | venue.timeZone.tz | division.id | division.name    | division.link          | conference.id | conference.name | conference.link          | franchise.franchiseId | franchise.teamName | franchise.link        |
|----:|:----------------------|:-----------------|:-------------|:---------------|:-------------|:----------------|:-------------|:-------------------------------------|------------:|:-------|:----------------------------------|:--------------------|:-------------|---------:|:---------------------|----------------------:|:------------------|------------:|:-----------------|:-----------------------|--------------:|:----------------|:-------------------------|----------------------:|:-------------------|:----------------------|
|   1 | New Jersey Devils     | /api/v1/teams/1  | NJD          | Devils         | New Jersey   | 1982            | New Jersey   | <http://www.newjerseydevils.com/>    |          23 | TRUE   | Prudential Center                 | /api/v1/venues/null | Newark       |       NA | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    23 | Devils             | /api/v1/franchises/23 |
|   2 | New York Islanders    | /api/v1/teams/2  | NYI          | Islanders      | New York     | 1972            | NY Islanders | <http://www.newyorkislanders.com/>   |          22 | TRUE   | Nassau Veterans Memorial Coliseum | /api/v1/venues/null | Uniondale    |       NA | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    22 | Islanders          | /api/v1/franchises/22 |
|   3 | New York Rangers      | /api/v1/teams/3  | NYR          | Rangers        | New York     | 1926            | NY Rangers   | <http://www.newyorkrangers.com/>     |          10 | TRUE   | Madison Square Garden             | /api/v1/venues/5054 | New York     |     5054 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    10 | Rangers            | /api/v1/franchises/10 |
|   4 | Philadelphia Flyers   | /api/v1/teams/4  | PHI          | Flyers         | Philadelphia | 1967            | Philadelphia | <http://www.philadelphiaflyers.com/> |          16 | TRUE   | Wells Fargo Center                | /api/v1/venues/5096 | Philadelphia |     5096 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    16 | Flyers             | /api/v1/franchises/16 |
|   5 | Pittsburgh Penguins   | /api/v1/teams/5  | PIT          | Penguins       | Pittsburgh   | 1967            | Pittsburgh   | <http://pittsburghpenguins.com/>     |          17 | TRUE   | PPG Paints Arena                  | /api/v1/venues/5034 | Pittsburgh   |     5034 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    17 | Penguins           | /api/v1/franchises/17 |
|   6 | Boston Bruins         | /api/v1/teams/6  | BOS          | Bruins         | Boston       | 1924            | Boston       | <http://www.bostonbruins.com/>       |           6 | TRUE   | TD Garden                         | /api/v1/venues/5085 | Boston       |     5085 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                     6 | Bruins             | /api/v1/franchises/6  |
|   7 | Buffalo Sabres        | /api/v1/teams/7  | BUF          | Sabres         | Buffalo      | 1970            | Buffalo      | <http://www.sabres.com/>             |          19 | TRUE   | KeyBank Center                    | /api/v1/venues/5039 | Buffalo      |     5039 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    19 | Sabres             | /api/v1/franchises/19 |
|   8 | Montréal Canadiens    | /api/v1/teams/8  | MTL          | Canadiens      | Montréal     | 1909            | Montréal     | <http://www.canadiens.com/>          |           1 | TRUE   | Bell Centre                       | /api/v1/venues/5028 | Montréal     |     5028 | America/Montreal     |                    -4 | EDT               |          28 | Scotia North     | /api/v1/divisions/28   |             6 | Eastern         | /api/v1/conferences/6    |                     1 | Canadiens          | /api/v1/franchises/1  |
|   9 | Ottawa Senators       | /api/v1/teams/9  | OTT          | Senators       | Ottawa       | 1990            | Ottawa       | <http://www.ottawasenators.com/>     |          30 | TRUE   | Canadian Tire Centre              | /api/v1/venues/5031 | Ottawa       |     5031 | America/New\_York    |                    -4 | EDT               |          28 | Scotia North     | /api/v1/divisions/28   |             6 | Eastern         | /api/v1/conferences/6    |                    30 | Senators           | /api/v1/franchises/30 |
|  10 | Toronto Maple Leafs   | /api/v1/teams/10 | TOR          | Maple Leafs    | Toronto      | 1917            | Toronto      | <http://www.mapleleafs.com/>         |           5 | TRUE   | Scotiabank Arena                  | /api/v1/venues/null | Toronto      |       NA | America/Toronto      |                    -4 | EDT               |          28 | Scotia North     | /api/v1/divisions/28   |             6 | Eastern         | /api/v1/conferences/6    |                     5 | Maple Leafs        | /api/v1/franchises/5  |
|  12 | Carolina Hurricanes   | /api/v1/teams/12 | CAR          | Hurricanes     | Carolina     | 1979            | Carolina     | <http://www.carolinahurricanes.com/> |          26 | TRUE   | PNC Arena                         | /api/v1/venues/5066 | Raleigh      |     5066 | America/New\_York    |                    -4 | EDT               |          26 | Discover Central | /api/v1/divisions/26   |             6 | Eastern         | /api/v1/conferences/6    |                    26 | Hurricanes         | /api/v1/franchises/26 |
|  13 | Florida Panthers      | /api/v1/teams/13 | FLA          | Panthers       | Florida      | 1993            | Florida      | <http://www.floridapanthers.com/>    |          33 | TRUE   | BB&T Center                       | /api/v1/venues/5027 | Sunrise      |     5027 | America/New\_York    |                    -4 | EDT               |          26 | Discover Central | /api/v1/divisions/26   |             6 | Eastern         | /api/v1/conferences/6    |                    33 | Panthers           | /api/v1/franchises/33 |
|  14 | Tampa Bay Lightning   | /api/v1/teams/14 | TBL          | Lightning      | Tampa Bay    | 1991            | Tampa Bay    | <http://www.tampabaylightning.com/>  |          31 | TRUE   | AMALIE Arena                      | /api/v1/venues/null | Tampa        |       NA | America/New\_York    |                    -4 | EDT               |          26 | Discover Central | /api/v1/divisions/26   |             6 | Eastern         | /api/v1/conferences/6    |                    31 | Lightning          | /api/v1/franchises/31 |
|  15 | Washington Capitals   | /api/v1/teams/15 | WSH          | Capitals       | Washington   | 1974            | Washington   | <http://www.washingtoncapitals.com/> |          24 | TRUE   | Capital One Arena                 | /api/v1/venues/5094 | Washington   |     5094 | America/New\_York    |                    -4 | EDT               |          25 | MassMutual East  | /api/v1/divisions/25   |             6 | Eastern         | /api/v1/conferences/6    |                    24 | Capitals           | /api/v1/franchises/24 |
|  16 | Chicago Blackhawks    | /api/v1/teams/16 | CHI          | Blackhawks     | Chicago      | 1926            | Chicago      | <http://www.chicagoblackhawks.com/>  |          11 | TRUE   | United Center                     | /api/v1/venues/5092 | Chicago      |     5092 | America/Chicago      |                    -5 | CDT               |          26 | Discover Central | /api/v1/divisions/26   |             5 | Western         | /api/v1/conferences/5    |                    11 | Blackhawks         | /api/v1/franchises/11 |
|  17 | Detroit Red Wings     | /api/v1/teams/17 | DET          | Red Wings      | Detroit      | 1926            | Detroit      | <http://www.detroitredwings.com/>    |          12 | TRUE   | Little Caesars Arena              | /api/v1/venues/5145 | Detroit      |     5145 | America/Detroit      |                    -4 | EDT               |          26 | Discover Central | /api/v1/divisions/26   |             6 | Eastern         | /api/v1/conferences/6    |                    12 | Red Wings          | /api/v1/franchises/12 |
|  18 | Nashville Predators   | /api/v1/teams/18 | NSH          | Predators      | Nashville    | 1997            | Nashville    | <http://www.nashvillepredators.com/> |          34 | TRUE   | Bridgestone Arena                 | /api/v1/venues/5030 | Nashville    |     5030 | America/Chicago      |                    -5 | CDT               |          26 | Discover Central | /api/v1/divisions/26   |             5 | Western         | /api/v1/conferences/5    |                    34 | Predators          | /api/v1/franchises/34 |
|  19 | St. Louis Blues       | /api/v1/teams/19 | STL          | Blues          | St. Louis    | 1967            | St Louis     | <http://www.stlouisblues.com/>       |          18 | TRUE   | Enterprise Center                 | /api/v1/venues/5076 | St. Louis    |     5076 | America/Chicago      |                    -5 | CDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    18 | Blues              | /api/v1/franchises/18 |
|  20 | Calgary Flames        | /api/v1/teams/20 | CGY          | Flames         | Calgary      | 1980            | Calgary      | <http://www.calgaryflames.com/>      |          21 | TRUE   | Scotiabank Saddledome             | /api/v1/venues/5075 | Calgary      |     5075 | America/Denver       |                    -6 | MDT               |          28 | Scotia North     | /api/v1/divisions/28   |             5 | Western         | /api/v1/conferences/5    |                    21 | Flames             | /api/v1/franchises/21 |
|  21 | Colorado Avalanche    | /api/v1/teams/21 | COL          | Avalanche      | Colorado     | 1979            | Colorado     | <http://www.coloradoavalanche.com/>  |          27 | TRUE   | Ball Arena                        | /api/v1/venues/5064 | Denver       |     5064 | America/Denver       |                    -6 | MDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    27 | Avalanche          | /api/v1/franchises/27 |
|  22 | Edmonton Oilers       | /api/v1/teams/22 | EDM          | Oilers         | Edmonton     | 1979            | Edmonton     | <http://www.edmontonoilers.com/>     |          25 | TRUE   | Rogers Place                      | /api/v1/venues/5100 | Edmonton     |     5100 | America/Edmonton     |                    -6 | MDT               |          28 | Scotia North     | /api/v1/divisions/28   |             5 | Western         | /api/v1/conferences/5    |                    25 | Oilers             | /api/v1/franchises/25 |
|  23 | Vancouver Canucks     | /api/v1/teams/23 | VAN          | Canucks        | Vancouver    | 1970            | Vancouver    | <http://www.canucks.com/>            |          20 | TRUE   | Rogers Arena                      | /api/v1/venues/5073 | Vancouver    |     5073 | America/Vancouver    |                    -7 | PDT               |          28 | Scotia North     | /api/v1/divisions/28   |             5 | Western         | /api/v1/conferences/5    |                    20 | Canucks            | /api/v1/franchises/20 |
|  24 | Anaheim Ducks         | /api/v1/teams/24 | ANA          | Ducks          | Anaheim      | 1993            | Anaheim      | <http://www.anaheimducks.com/>       |          32 | TRUE   | Honda Center                      | /api/v1/venues/5046 | Anaheim      |     5046 | America/Los\_Angeles |                    -7 | PDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    32 | Ducks              | /api/v1/franchises/32 |
|  25 | Dallas Stars          | /api/v1/teams/25 | DAL          | Stars          | Dallas       | 1967            | Dallas       | <http://www.dallasstars.com/>        |          15 | TRUE   | American Airlines Center          | /api/v1/venues/5019 | Dallas       |     5019 | America/Chicago      |                    -5 | CDT               |          26 | Discover Central | /api/v1/divisions/26   |             5 | Western         | /api/v1/conferences/5    |                    15 | Stars              | /api/v1/franchises/15 |
|  26 | Los Angeles Kings     | /api/v1/teams/26 | LAK          | Kings          | Los Angeles  | 1967            | Los Angeles  | <http://www.lakings.com/>            |          14 | TRUE   | STAPLES Center                    | /api/v1/venues/5081 | Los Angeles  |     5081 | America/Los\_Angeles |                    -7 | PDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    14 | Kings              | /api/v1/franchises/14 |
|  28 | San Jose Sharks       | /api/v1/teams/28 | SJS          | Sharks         | San Jose     | 1990            | San Jose     | <http://www.sjsharks.com/>           |          29 | TRUE   | SAP Center at San Jose            | /api/v1/venues/null | San Jose     |       NA | America/Los\_Angeles |                    -7 | PDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    29 | Sharks             | /api/v1/franchises/29 |
|  29 | Columbus Blue Jackets | /api/v1/teams/29 | CBJ          | Blue Jackets   | Columbus     | 1997            | Columbus     | <http://www.bluejackets.com/>        |          36 | TRUE   | Nationwide Arena                  | /api/v1/venues/5059 | Columbus     |     5059 | America/New\_York    |                    -4 | EDT               |          26 | Discover Central | /api/v1/divisions/26   |             6 | Eastern         | /api/v1/conferences/6    |                    36 | Blue Jackets       | /api/v1/franchises/36 |
|  30 | Minnesota Wild        | /api/v1/teams/30 | MIN          | Wild           | Minnesota    | 1997            | Minnesota    | <http://www.wild.com/>               |          37 | TRUE   | Xcel Energy Center                | /api/v1/venues/5098 | St. Paul     |     5098 | America/Chicago      |                    -5 | CDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    37 | Wild               | /api/v1/franchises/37 |
|  52 | Winnipeg Jets         | /api/v1/teams/52 | WPG          | Jets           | Winnipeg     | 2011            | Winnipeg     | <http://winnipegjets.com/>           |          35 | TRUE   | Bell MTS Place                    | /api/v1/venues/5058 | Winnipeg     |     5058 | America/Winnipeg     |                    -5 | CDT               |          28 | Scotia North     | /api/v1/divisions/28   |             5 | Western         | /api/v1/conferences/5    |                    35 | Jets               | /api/v1/franchises/35 |
|  53 | Arizona Coyotes       | /api/v1/teams/53 | ARI          | Coyotes        | Arizona      | 1979            | Arizona      | <http://www.arizonacoyotes.com/>     |          28 | TRUE   | Gila River Arena                  | /api/v1/venues/5043 | Glendale     |     5043 | America/Phoenix      |                    -7 | MST               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    28 | Coyotes            | /api/v1/franchises/28 |
|  54 | Vegas Golden Knights  | /api/v1/teams/54 | VGK          | Golden Knights | Vegas        | 2016            | Vegas        | <http://www.vegasgoldenknights.com/> |          38 | TRUE   | T-Mobile Arena                    | /api/v1/venues/5178 | Las Vegas    |     5178 | America/Los\_Angeles |                    -7 | PDT               |          27 | Honda West       | /api/v1/divisions/27   |             5 | Western         | /api/v1/conferences/5    |                    38 | Golden Knights     | /api/v1/franchises/38 |
|  55 | Seattle Kraken        | /api/v1/teams/55 | SEA          | Kraken         | Seattle      | NA              | NA           | <https://www.nhl.com/seattle>        |          39 | FALSE  | NA                                | NA                  | NA           |       NA | NA                   |                    NA | NA                |          NA | NA               | /api/v1/divisions/null |            NA | NA              | /api/v1/conferences/null |                    39 | Kraken             | /api/v1/franchises/39 |

</td>
</tr>
</tbody>
</table>

``` r
#wrapper function
wrapper_url = "https://statsapi.web.nhl.com/api/v1"
```

``` r
get_wrapper = function(){
  # Not sure if I am doing this correctly
  # Probably not the most efficient way to do it
  team.roster_full_url = paste0(wrapper_url, "/teams?expand=team.roster=")
  person.names_full_url = paste0(wrapper_url, "/teams?expand=person.names=")
  team.schedule.next_full_url = paste0(wrapper_url, "/teams?expand=team.schedule.next=")
  team.schedule.previous_full_url = paste0(wrapper_url, "/teams?expand=team.schedule.previous=")
  team.stats_full_url = paste0(wrapper_url, "/teams?expand=team.stats=")
  #team_roster&season_full_url = paste0(wrapper_url, "/teams?expand=team.roster&season=")
  team.Id_full_url = paste0(wrapper_url, "/teams?expand=teamId=")
  stats_full_url = paste0(wrapper_url, "/teams?expand=stats=")
  
  team.roster_text = content(GET(url=team.roster_full_url), "text")
  person.names_text = content(GET(url=person.names_full_url), "text")
  team.schedule.next_text = content(GET(url=team.schedule.next_full_url), "text")
  team.schedule.previous_text = content(GET(url=team.schedule.previous_full_url), "text")
  team.stats_text = content(GET(url=team.stats_full_url), "text")
  #team_roster&season_text = content(GET(url=team_roster&season_full_url), "text")
  team.Id_text = content(GET(url=team.Id_full_url), "text")
  stats_text = content(GET(url=stats_full_url), "text")
  
  
  team.roster_json = fromJSON(team.roster_text, flatten = T)
  person.names_json = fromJSON(person.names_text, flatten = T)
  team.schedule.next_json = fromJSON(team.schedule.next_text, flatten = T)
  team.schedule.previous_json = fromJSON(team.schedule.previous_text, flatten = T)
  team.stats_json = fromJSON(team.stats_text, flatten = T)
  #team_roster&season_json = fromJSON(team_roster&season_text, flatten = T)
  team.Id_json = fromJSON(team.Id_text, flatten = T)
  stats_json = fromJSON(stats_text, flatten = T)
  wrapper_json <- list(team.roster_json,person.names_json, team.schedule.next_json,team.schedule.previous_json, team.stats_json, team.Id_json, stats_json)
  #return(wrapper_json)
  #wrap2 <- list(team.roster[2],person.names[2],)
  #team.stats2 <- team.stats[2]
  #return(team.stats2)
  #return(team.stats_json)
}
```

``` r
#Yeah, I am going stop here today, because I do not think I am doing the wrapper function correctly.
wrap = get_wrapper()
```

## More functions

## Wrapper functions

# Exploratory Data Analysis
