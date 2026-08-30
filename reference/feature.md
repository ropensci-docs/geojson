# feature class

feature class

## Usage

``` r
feature(x)
```

## Arguments

- x:

  input

## Details

Feature objects:

- A feature object must have a member with the name "geometry". The
  value of the geometry member is a geometry object as defined above or
  a JSON null value.

- A feature object must have a member with the name "properties". The
  value of the properties member is an object (any JSON object or a JSON
  null value).

- If a feature has a commonly used identifier, that identifier should be
  included as a member of the feature object with the name "id".

## Examples

``` r
# point -> feature
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
point(x) %>% feature()
#> <Feature> 
#>   type:  Point 
#>   coordinates:  [100.0,0.0] 

# multipoint -> feature
x <- '{"type": "MultiPoint", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }'
multipoint(x) %>% feature()
#> <Feature> 
#>   type:  MultiPoint 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 

# linestring -> feature
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }'
linestring(x) %>% feature()
#> <Feature> 
#>   type:  LineString 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 

# multilinestring -> feature
x <- '{ "type": "MultiLineString",
 "coordinates": [ [ [100.0, 0.0], [101.0, 1.0] ], [ [102.0, 2.0], [103.0, 3.0] ] ] }'
multilinestring(x) %>% feature()
#> <Feature> 
#>   type:  MultiLineString 
#>   coordinates:  [[[100.0,0.0],[101.0,1.0]],[[102.0,2.0],[103.0,3.0]]] 

# add to a data.frame
library('tibble')
tibble(a = 1:5, b = list(multilinestring(x)))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <gmltlnst [1]>
#> 2     2 <gmltlnst [1]>
#> 3     3 <gmltlnst [1]>
#> 4     4 <gmltlnst [1]>
#> 5     5 <gmltlnst [1]>
```
