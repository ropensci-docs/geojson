# Write geojson to disk

Write geojson to disk

## Usage

``` r
geo_write(x, file)
```

## Arguments

- x:

  input, an object of class `geojson`

- file:

  (character) a file path, or connection

## Details

Wrapper around
[`jsonlite::toJSON()`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html)
and [`cat`](https://rdrr.io/r/base/cat.html)

## Examples

``` r
file <- tempfile(fileext = ".geojson")
geo_write(
  point('{ "type": "Point", "coordinates": [100.0, 0.0] }'),
  file
)
readLines(file)
#> [1] "{"                           "  \"type\": \"Point\","     
#> [3] "  \"coordinates\": [100, 0]" "} "                         
unlink(file)
```
