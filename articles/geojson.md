# geojson package classes

The `geojson` package has a function to create a GeoJSON class matching
all the GeoJSON data types:

- [`point()`](https://docs.ropensci.org/geojson/reference/point.md) -
  Point
- [`multipoint()`](https://docs.ropensci.org/geojson/reference/multipoint.md) -
  MultiPoint
- [`linestring()`](https://docs.ropensci.org/geojson/reference/linestring.md) -
  LineString
- [`multilinestring()`](https://docs.ropensci.org/geojson/reference/multilinestring.md) -
  MultiLineString
- [`polygon()`](https://docs.ropensci.org/geojson/reference/polygon.md) -
  Polygon
- [`multipolygon()`](https://docs.ropensci.org/geojson/reference/multipolygon.md) -
  MultiPolygon
- [`feature()`](https://docs.ropensci.org/geojson/reference/feature.md) -
  Feature
- [`featurecollection()`](https://docs.ropensci.org/geojson/reference/featurecollection.md) -
  FeatureCollection
- [`geometrycollection()`](https://docs.ropensci.org/geojson/reference/geometrycollection.md) -
  GeometryCollection

The following are some examples of their usage.

``` r

library("geojson")
```

## point

``` r

(x <- point('{ "type": "Point", "coordinates": [100.0, 0.0] }'))
#> <Point> 
#>   coordinates:  [100.0,0.0]
class(x)
#> [1] "geopoint" "geojson"
attributes(x)
#> $class
#> [1] "geopoint" "geojson" 
#> 
#> $coords
#> [1] "[100.0,0.0]"
```

## multipoint

``` r

multipoint('{"type": "MultiPoint", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }')
#> <MultiPoint> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]]
```

## linestring

``` r

linestring('{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }')
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]]
```

## multilinestring

``` r

str <- '{ "type": "MultiLineString",
  "coordinates": [ [ [100.0, 0.0], [101.0, 1.0] ], [ [102.0, 2.0], [103.0, 3.0] ] ] }'
multilinestring(str)
#> <MultiLineString> 
#>   no. lines:  2 
#>   no. nodes / line:  2, 2 
#>   coordinates:  [[[100.0,0.0],[101.0,1.0]],[[102.0,2.0],[103.0,3.0]]]
```

## polygon

``` r

str <- '{ "type": "Polygon",
 "coordinates": [
   [ [100.0, 0.0], [100.0, 1.0], [101.0, 1.0], [101.0, 0.0], [100.0, 0.0] ]
   ]
}'
polygon(str)
#> <Polygon> 
#>   no. lines:  1 
#>   no. holes:  0 
#>   no. nodes / line:  5 
#>   coordinates:  [[[100.0,0.0],[100.0,1.0],[101.0,1.0],[101.0,0.0],[100.0,0.0]]]
```

## multipolygon

``` r

str <- '{ "type": "MultiPolygon",
  "coordinates": [
   [[[102.0, 2.0], [103.0, 2.0], [103.0, 3.0], [102.0, 3.0], [102.0, 2.0]]],
   [[[100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0]],
   [[100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2]]]
  ]
}'
multipolygon(str)
#> <MultiPolygon> 
#>   no. polygons:  2 
#>   coordinates:  [[[[102.0,2.0],[103.0,2.0],[103.0,3.0],[102.0,3.0],[102.0,2.0]]],[[[10 ...
```

## feature

From `geopoint` class

``` r

pt <- point('{ "type": "Point", "coordinates": [100.0, 0.0] }')
feature(pt)
#> <Feature> 
#>   type:  Point 
#>   coordinates:  [100.0,0.0]
```

From character string

``` r

str <- "{ \"type\": \"Feature\", \"properties\": {}, \"geometry\": { \"type\": \"Point\", \"coordinates\": [100.0, 0.0] } }"
feature(str)
#> <Feature> 
#>   type:  Point 
#>   coordinates:  [100.0,0.0]
```

## featurecollection

From feature

``` r

pt %>% feature() %>% featurecollection()
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  1 
#>   features (1st 5):  Point
```

From string

``` r

file <- system.file("examples", 'featurecollection1.geojson', package = "geojson")
str <- paste0(readLines(file), collapse = " ")
featurecollection(str)
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  1 
#>   features (1st 5):  GeometryCollection
```

## geometrycollection

``` r

str <- '{
 "type": "GeometryCollection",
 "geometries": [
   {
     "type": "Point",
     "coordinates": [100.0, 0.0]
   },
   {
     "type": "LineString",
     "coordinates": [ [101.0, 0.0], [102.0, 1.0] ]
   }
  ]
}'
geometrycollection(str)
#> <GeometryCollection> 
#>   geometries (n): 2 
#>   geometries (geometry / length):
#>     Point / 2
#>     LineString / 2
```
