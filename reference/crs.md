# Add or get CRS

Add or get CRS

## Usage

``` r
crs_add(x, crs)

crs_get(x)
```

## Arguments

- x:

  An object of class `geojson`

- crs:

  (character) a CRS string. required.

## Details

According to RFC 7946
(<https://datatracker.ietf.org/doc/html/rfc7946#page-12>) the CRS for
all GeoJSON objects must be WGS-84, equivalent to
`urn:ogc:def:crs:OGC::CRS84`. And lat/long must be in decimal degrees.

Given the above, but considering that GeoJSON blobs exist that have CRS
attributes in them, we provide CRS helpers here. But moving forward
these are not likely to be used much.

## References

<https://github.com/OSGeo/PROJ>,
<https://geojson.org/geojson-spec.html#coordinate-reference-system-objects>

## Examples

``` r
x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ]
  ]
}'

# add crs
crs <- '{"type": "name",
 "properties": {
     "name": "urn:ogc:def:crs:OGC:1.3:CRS84"
}}'
x %>% feature() %>% crs_add(crs)
#> {
#>     "type": "Feature",
#>     "properties": {
#> 
#>     },
#>     "geometry": {
#>         "type": "Polygon",
#>         "coordinates": [
#>             [
#>                 [
#>                     100.0,
#>                     0.0
#>                 ],
#>                 [
#>                     101.0,
#>                     0.0
#>                 ],
#>                 [
#>                     101.0,
#>                     1.0
#>                 ],
#>                 [
#>                     100.0,
#>                     1.0
#>                 ],
#>                 [
#>                     100.0,
#>                     0.0
#>                 ]
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

# get crs
z <- x %>% feature() %>% crs_add(crs)
crs_get(z)
#> $type
#> [1] "name"
#> 
#> $properties
#> $properties$name
#> [1] "urn:ogc:def:crs:OGC:1.3:CRS84"
#> 
#> 
```
