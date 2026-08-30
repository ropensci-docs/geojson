# Get geometry type

Get geometry type

## Usage

``` r
geo_type(x)
```

## Arguments

- x:

  input, an object of class `geojson`

## Examples

``` r
geo_type(point('{ "type": "Point", "coordinates": [100.0, 0.0] }'))
#> [1] "Point"

x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [100.0, 1.0], [101.0, 1.0], [101.0, 0.0], [100.0, 0.0] ]
  ]
}'
poly <- polygon(x)

geo_type(poly)
#> [1] "Polygon"
```
