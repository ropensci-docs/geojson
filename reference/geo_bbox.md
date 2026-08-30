# Calculate a bounding box

Calculate a bounding box

## Usage

``` r
geo_bbox(x)
```

## Arguments

- x:

  an object of class geojson

## Value

a vector of four doubles: min lon, min lat, max lon, max lat

## Details

Supports inputs of type: character, point, multipoint, linestring,
multilinestring, polygon, multipoygon, feature, and featurecollection

On character inputs, we lint the input to make sure it's proper JSON and
GeoJSON, then caculate the bounding box

## Examples

``` r
# point
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
(y <- point(x))
#> <Point> 
#>   coordinates:  [100.0,0.0] 
geo_bbox(y)
#> [1] 100   0 100   0
y %>% feature() %>% geo_bbox()
#> [1] 100   0 100   0

# multipoint
x <- '{"type": "MultiPoint", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }'
(y <- multipoint(x))
#> <MultiPoint> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
geo_bbox(y)
#> [1] 100   0 101   1
y %>% feature() %>% geo_bbox()
#> [1] 100   0 101   1

# linestring
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
geo_bbox(y)
#> [1] 100   0 101   1
y %>% feature() %>% geo_bbox()
#> [1] 100   0 101   1
file <- system.file("examples", 'linestring_one.geojson',
  package = "geojson")
con <- file(file)
str <- paste0(readLines(con), collapse = " ")
(y <- linestring(str))
#> <LineString> 
#>   coordinates:  [[109.96,54.50,0.0],[109.95,54.51,0.0],[109.96,54.52,0.0],[109.96,54.5 ... 
geo_bbox(y)
#> [1] 109.95  54.48 110.00  54.52
y %>% feature() %>% geo_bbox()
#> [1] 109.95  54.48 110.00  54.52
close(con)

if (FALSE) { # \dontrun{
# multilinestring
x <- '{ "type": "MultiLineString",
 "coordinates": [ [ [100.0, 0.0], [101.0, 1.0] ], [ [102.0, 2.0],
 [103.0, 3.0] ] ] }'
(y <- multilinestring(x))
geo_bbox(y)
y %>% feature() %>% geo_bbox()

# polygon
x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ]
  ]
}'
(y <- polygon(x))
geo_bbox(y)
y %>% feature() %>% geo_bbox()

# multipolygon
x <- '{ "type": "MultiPolygon",
"coordinates": [
  [[[102.0, 2.0], [103.0, 2.0], [103.0, 3.0], [102.0, 3.0], [102.0, 2.0]]],
  [[[100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0]],
  [[100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2]]]
  ]
}'
(y <- multipolygon(x))
geo_bbox(y)
y %>% feature() %>% geo_bbox()

# featurecollection
file <- system.file("examples", 'featurecollection2.geojson',
  package = "geojson")
str <- paste0(readLines(file), collapse = " ")
x <- featurecollection(str)
geo_bbox(x)

# character
file <- system.file("examples", 'featurecollection2.geojson',
  package = "geojson")
str <- paste0(readLines(file), collapse = " ")
geo_bbox(str)

# json
library('jsonlite')
geo_bbox(toJSON(fromJSON(str), auto_unbox = TRUE))
} # }
```
