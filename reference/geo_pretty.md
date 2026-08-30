# Pretty print geojson

Pretty print geojson

## Usage

``` r
geo_pretty(x)
```

## Arguments

- x:

  input, an object of class `geojson`

## Details

Wrapper around
[`prettify`](https://jeroen.r-universe.dev/jsonlite/reference/prettify.html)

## Examples

``` r
geo_pretty(point('{ "type": "Point", "coordinates": [100.0, 0.0] }'))
#> {
#>     "type": "Point",
#>     "coordinates": [
#>         100.0,
#>         0.0
#>     ]
#> }
#>  

x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [100.0, 1.0], [101.0, 1.0], [101.0, 0.0], [100.0, 0.0] ]
  ]
}'
poly <- polygon(x)
geo_pretty(poly)
#> {
#>     "type": "Polygon",
#>     "coordinates": [
#>         [
#>             [
#>                 100.0,
#>                 0.0
#>             ],
#>             [
#>                 100.0,
#>                 1.0
#>             ],
#>             [
#>                 101.0,
#>                 1.0
#>             ],
#>             [
#>                 101.0,
#>                 0.0
#>             ],
#>             [
#>                 100.0,
#>                 0.0
#>             ]
#>         ]
#>     ]
#> }
#>  
```
