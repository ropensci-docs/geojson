# geojson operations

The `geojson` package has functions to do basic operations on GeoJSON
classes.

``` r

library("geojson")
```

First, let’s make a GeoJSON object

``` r

x <- '{
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
(y <- geometrycollection(x))
#> <GeometryCollection> 
#>   geometries (n): 2 
#>   geometries (geometry / length):
#>     Point / 2
#>     LineString / 2
```

### inspect the object

Get the string

``` r

y[[1]]
#> [1] "{\n \"type\": \"GeometryCollection\",\n \"geometries\": [\n   {\n     \"type\": \"Point\",\n     \"coordinates\": [100.0, 0.0]\n   },\n   {\n     \"type\": \"LineString\",\n     \"coordinates\": [ [101.0, 0.0], [102.0, 1.0] ]\n   }\n  ]\n}"
```

Get the type

``` r

geo_type(y)
#> [1] "GeometryCollection"
```

Pretty print the geojson

``` r

geo_pretty(y)
#> {
#>     "type": "GeometryCollection",
#>     "geometries": [
#>         {
#>             "type": "Point",
#>             "coordinates": [
#>                 100.0,
#>                 0.0
#>             ]
#>         },
#>         {
#>             "type": "LineString",
#>             "coordinates": [
#>                 [
#>                     101.0,
#>                     0.0
#>                 ],
#>                 [
#>                     102.0,
#>                     1.0
#>                 ]
#>             ]
#>         }
#>     ]
#> }
#> 
```

Write to disk

``` r

geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "GeometryCollection"
#> 
#> $geometries
#> $geometries[[1]]
#> $geometries[[1]]$type
#> [1] "Point"
#> 
#> $geometries[[1]]$coordinates
#> $geometries[[1]]$coordinates[[1]]
#> [1] 100
#> 
#> $geometries[[1]]$coordinates[[2]]
#> [1] 0
#> 
#> 
#> 
#> $geometries[[2]]
#> $geometries[[2]]$type
#> [1] "LineString"
#> 
#> $geometries[[2]]$coordinates
#> $geometries[[2]]$coordinates[[1]]
#> $geometries[[2]]$coordinates[[1]][[1]]
#> [1] 101
#> 
#> $geometries[[2]]$coordinates[[1]][[2]]
#> [1] 0
#> 
#> 
#> $geometries[[2]]$coordinates[[2]]
#> $geometries[[2]]$coordinates[[2]][[1]]
#> [1] 102
#> 
#> $geometries[[2]]$coordinates[[2]][[2]]
#> [1] 1
```

## properties

Add properties

``` r

x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
res <- linestring(x) %>% feature() %>% properties_add(population = 1000)
res
#> <Feature> 
#>   type:  LineString 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]]
```

Get a property

``` r

properties_get(res, property = 'population')
#> 1000
```

## crs

Add crs

``` r

crs <- '{
  "type": "name",
  "properties": {
     "name": "urn:ogc:def:crs:OGC:1.3:CRS84"
  }
}'
z <- x %>% feature() %>% crs_add(crs)
z
#> {
#>     "type": "Feature",
#>     "properties": {
#> 
#>     },
#>     "geometry": {
#>         "type": "LineString",
#>         "coordinates": [
#>             [
#>                 100.0,
#>                 0.0
#>             ],
#>             [
#>                 101.0,
#>                 1.0
#>             ]
#>         ]
#>     },
#>     "crs": {
#>         "type": "name",
#>         "properties": {
#>             "name": "urn:ogc:def:crs:OGC:1.3:CRS84"
#>         }
#>     }
#> }
```

Get crs

``` r

crs_get(z)
#> $type
#> [1] "name"
#> 
#> $properties
#> $properties$name
#> [1] "urn:ogc:def:crs:OGC:1.3:CRS84"
```

## bbox

Add bbox - by default, if you don’t pass a bbox into
[`bbox_add()`](https://docs.ropensci.org/geojson/reference/bbox.md) we
attempt to calculate the bbox for you. You can also pass in your own
bbox.

``` r

tt <- x %>% feature() %>% bbox_add()
tt
#> {
#>     "type": "Feature",
#>     "properties": {
#> 
#>     },
#>     "geometry": {
#>         "type": "LineString",
#>         "coordinates": [
#>             [
#>                 100.0,
#>                 0.0
#>             ],
#>             [
#>                 101.0,
#>                 1.0
#>             ]
#>         ]
#>     },
#>     "bbox": [
#>         100,
#>         0,
#>         101,
#>         1
#>     ]
#> }
```

Get bbox

``` r

bbox_get(tt)
#> [1] 100   0 101   1
```

## geojson in data.frame’s

It’s really easy to put `geojson` class objects into data.frame’s as
well.

The ideal solution is to put them into `tbl`’s (see the `tibble`
package)

Make a `point`

``` r

x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
(pt <- point(x))
#> <Point> 
#>   coordinates:  [100.0,0.0]
```

Put the point into a `tbl`

``` r

library("tibble")
data_frame(a = 1:5, b = list(pt))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <geopoint [1]>
#> 2     2 <geopoint [1]>
#> 3     3 <geopoint [1]>
#> 4     4 <geopoint [1]>
#> 5     5 <geopoint [1]>
```

Another object, here a `multilinestring`

``` r

x <- '{ "type": "MultiLineString",
  "coordinates": [ [ [100.0, 0.0], [101.0, 1.0] ], [ [102.0, 2.0], [103.0, 3.0] ] ] }'
(mls <- multilinestring(x))
#> <MultiLineString> 
#>   no. lines:  2 
#>   no. nodes / line:  2, 2 
#>   coordinates:  [[[100.0,0.0],[101.0,1.0]],[[102.0,2.0],[103.0,3.0]]]
```

Put into a `tbl`

``` r

data_frame(a = 1:5, b = list(mls))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <gmltlnst [1]>
#> 2     2 <gmltlnst [1]>
#> 3     3 <gmltlnst [1]>
#> 4     4 <gmltlnst [1]>
#> 5     5 <gmltlnst [1]>
```

Put the `point` and `multilinestring` into the same `tbl`

``` r

(df <- data_frame(a = 1:5, b = list(pt), c = list(mls)))
#> # A tibble: 5 × 3
#>       a b              c             
#>   <int> <list>         <list>        
#> 1     1 <geopoint [1]> <gmltlnst [1]>
#> 2     2 <geopoint [1]> <gmltlnst [1]>
#> 3     3 <geopoint [1]> <gmltlnst [1]>
#> 4     4 <geopoint [1]> <gmltlnst [1]>
#> 5     5 <geopoint [1]> <gmltlnst [1]>
```

And you can pull the geojson back out

``` r

df$b
#> [[1]]
#> <Point> 
#>   coordinates:  [100.0,0.0] 
#> 
#> [[2]]
#> <Point> 
#>   coordinates:  [100.0,0.0] 
#> 
#> [[3]]
#> <Point> 
#>   coordinates:  [100.0,0.0] 
#> 
#> [[4]]
#> <Point> 
#>   coordinates:  [100.0,0.0] 
#> 
#> [[5]]
#> <Point> 
#>   coordinates:  [100.0,0.0]
df$b[[1]]
#> <Point> 
#>   coordinates:  [100.0,0.0]
```
