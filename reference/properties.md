# Add or get properties

Add or get properties

## Usage

``` r
properties_add(x, ..., .list = NULL)

properties_get(x, property)
```

## Arguments

- x:

  An object of class `geojson`

- ...:

  Properties to be added, supports NSE as well as SE

- .list:

  a named list of properties to add. must be named

- property:

  (character) property name

## References

<https://geojson.org/geojson-spec.html>

## Examples

``` r
# add properties
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
y %>% feature() %>% properties_add(population = 1000)
#> <Feature> 
#>   type:  LineString 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 

## add with a named list already created
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
props <- list(population = 1000, temperature = 89, size = 5)
y %>% feature() %>% properties_add(.list = props)
#> <Feature> 
#>   type:  LineString 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 

## combination of NSE and .list
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
props <- list(population = 1000, temperature = 89, size = 5)
y %>% feature() %>% properties_add(stuff = 4, .list = props)
#> <Feature> 
#>   type:  LineString 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 

# features to featurecollection
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
point(x) %>%
  feature() %>%
  featurecollection() %>%
  properties_add(population = 10)
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  1 
#>   features (1st 5):  Point 

# get property
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
x <- y %>% feature() %>% properties_add(population = 1000)
properties_get(x, property = 'population')
#> 1000
```
