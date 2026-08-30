# featurecollection class

featurecollection class

## Usage

``` r
featurecollection(x)
```

## Arguments

- x:

  input

## Examples

``` r
file <- system.file("examples", 'featurecollection1.geojson',
  package = "geojson")
file <- system.file("examples", 'featurecollection2.geojson',
  package = "geojson")
str <- paste0(readLines(file), collapse = " ")
(y <- featurecollection(str))
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  3 
#>   features (1st 5):  Point, Point, Point 
geo_type(y)
#> [1] "FeatureCollection"
geo_pretty(y)
#> {
#>     "type": "FeatureCollection",
#>     "features": [
#>         {
#>             "type": "Feature",
#>             "id": 0,
#>             "properties": {
#>                 "NOME": "Sec de segunrança",
#>                 "URL": "http://www.theatermania.com/new-york/theaters/45th-street-theatre_2278/",
#>                 "ADDRESS1": "354 West 45th Street",
#>                 "CIDADE": "Goiânia",
#>                 "CEP": 74250010
#>             },
#>             "geometry": {
#>                 "type": "Point",
#>                 "coordinates": [
#>                     -49.256240,
#>                     -16.689612
#>                 ]
#>             }
#>         },
#>         {
#>             "type": "Feature",
#>             "id": 1,
#>             "properties": {
#>                 "NOME": "Teste",
#>                 "URL": "http://www.bestofoffbroadway.com/theaters/47streettheatre.html",
#>                 "ADDRESS1": "304 West 47th Street",
#>                 "CIDADE": "New York",
#>                 "ZIP": 74250010
#>             },
#>             "geometry": {
#>                 "type": "Point",
#>                 "coordinates": [
#>                     -49.276240,
#>                     -16.655612
#>                 ]
#>             }
#>         },
#>         {
#>             "type": "Feature",
#>             "id": 3,
#>             "properties": {
#>                 "NOME": "Delacorte Theater",
#>                 "URL": "http://www.centralpark.com/pages/attractions/delacorte-theatre.html",
#>                 "ADDRESS1": "Central Park - Mid-Park at 80th Street",
#>                 "CIDADE": "New York",
#>                 "ZIP": 74250010
#>             },
#>             "geometry": {
#>                 "type": "Point",
#>                 "coordinates": [
#>                     -49.277263,
#>                     -16.679057
#>                 ]
#>             }
#>         }
#>     ]
#> }
#>  
geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "FeatureCollection"
#> 
#> $features
#> $features[[1]]
#> $features[[1]]$type
#> [1] "Feature"
#> 
#> $features[[1]]$id
#> [1] 0
#> 
#> $features[[1]]$properties
#> $features[[1]]$properties$NOME
#> [1] "Sec de segunrança"
#> 
#> $features[[1]]$properties$URL
#> [1] "http://www.theatermania.com/new-york/theaters/45th-street-theatre_2278/"
#> 
#> $features[[1]]$properties$ADDRESS1
#> [1] "354 West 45th Street"
#> 
#> $features[[1]]$properties$CIDADE
#> [1] "Goiânia"
#> 
#> $features[[1]]$properties$CEP
#> [1] 74250010
#> 
#> 
#> $features[[1]]$geometry
#> $features[[1]]$geometry$type
#> [1] "Point"
#> 
#> $features[[1]]$geometry$coordinates
#> $features[[1]]$geometry$coordinates[[1]]
#> [1] -49.2562
#> 
#> $features[[1]]$geometry$coordinates[[2]]
#> [1] -16.6896
#> 
#> 
#> 
#> 
#> $features[[2]]
#> $features[[2]]$type
#> [1] "Feature"
#> 
#> $features[[2]]$id
#> [1] 1
#> 
#> $features[[2]]$properties
#> $features[[2]]$properties$NOME
#> [1] "Teste"
#> 
#> $features[[2]]$properties$URL
#> [1] "http://www.bestofoffbroadway.com/theaters/47streettheatre.html"
#> 
#> $features[[2]]$properties$ADDRESS1
#> [1] "304 West 47th Street"
#> 
#> $features[[2]]$properties$CIDADE
#> [1] "New York"
#> 
#> $features[[2]]$properties$ZIP
#> [1] 74250010
#> 
#> 
#> $features[[2]]$geometry
#> $features[[2]]$geometry$type
#> [1] "Point"
#> 
#> $features[[2]]$geometry$coordinates
#> $features[[2]]$geometry$coordinates[[1]]
#> [1] -49.2762
#> 
#> $features[[2]]$geometry$coordinates[[2]]
#> [1] -16.6556
#> 
#> 
#> 
#> 
#> $features[[3]]
#> $features[[3]]$type
#> [1] "Feature"
#> 
#> $features[[3]]$id
#> [1] 3
#> 
#> $features[[3]]$properties
#> $features[[3]]$properties$NOME
#> [1] "Delacorte Theater"
#> 
#> $features[[3]]$properties$URL
#> [1] "http://www.centralpark.com/pages/attractions/delacorte-theatre.html"
#> 
#> $features[[3]]$properties$ADDRESS1
#> [1] "Central Park - Mid-Park at 80th Street"
#> 
#> $features[[3]]$properties$CIDADE
#> [1] "New York"
#> 
#> $features[[3]]$properties$ZIP
#> [1] 74250010
#> 
#> 
#> $features[[3]]$geometry
#> $features[[3]]$geometry$type
#> [1] "Point"
#> 
#> $features[[3]]$geometry$coordinates
#> $features[[3]]$geometry$coordinates[[1]]
#> [1] -49.2773
#> 
#> $features[[3]]$geometry$coordinates[[2]]
#> [1] -16.6791
#> 
#> 
#> 
#> 
#> 
unlink(f)

# add to a data.frame
library('tibble')
tibble(a = 1:5, b = list(y))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <gftrcllc [1]>
#> 2     2 <gftrcllc [1]>
#> 3     3 <gftrcllc [1]>
#> 4     4 <gftrcllc [1]>
#> 5     5 <gftrcllc [1]>

# features to featurecollection
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
point(x) %>% feature() %>% featurecollection()
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  1 
#>   features (1st 5):  Point 

## all points
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
y <- '{ "type": "Point", "coordinates": [100.0, 50.0] }'
featls <- lapply(list(x, y), function(z) feature(point(z)))
featurecollection(featls)
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  2 
#>   features (1st 5):  Point, Point 
```
