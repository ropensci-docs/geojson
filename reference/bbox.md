# Add or get bounding box

Add or get bounding box

## Usage

``` r
bbox_add(x, bbox = NULL)

bbox_get(x)
```

## Arguments

- x:

  An object of class `geojson`

- bbox:

  (numeric) a vector or list of length 4 for a 2D bounding box or length
  6 for a 3D bounding box. If `NULL`, the bounding box is calculated for
  you

## Value

- bbox_add: an object of class jqson/character from jqr

- bbox_get: a bounding box, of the form `[west, south, east, north]` for
  2D or of the form
  `[west, south, min-altitude, east, north, max-altitude]` for 3D

## Details

Note that `bbox_get` outputs the bbox if it exists, but does not
calculate it from the geojson. See
[`geo_bbox`](https://docs.ropensci.org/geojson/reference/geo_bbox.md) to
calculate a bounding box. Bounding boxes can be 2D or 3D.

## References

<https://datatracker.ietf.org/doc/html/rfc7946#section-5>

## Examples

``` r
# make a polygon
x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ]
  ]
}'
(y <- polygon(x))
#> <Polygon> 
#>   no. lines:  1 
#>   no. holes:  0 
#>   no. nodes / line:  5 
#>   coordinates:  [[[100.0,0.0],[101.0,0.0],[101.0,1.0],[100.0,1.0],[100.0,0.0]]] 

# add bbox - without an input, we figure out the 2D bbox for you
y %>% feature() %>% bbox_add()
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
#>     "bbox": [
#>         100,
#>         0,
#>         101,
#>         1
#>     ]
#> }
## 2D bbox
y %>% feature() %>% bbox_add(c(100.0, -10.0, 105.0, 10.0))
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
#>     "bbox": [
#>         100,
#>         -10,
#>         105,
#>         10
#>     ]
#> }
## 3D bbox
y %>% feature() %>% bbox_add(c(100.0, -10.0, 3, 105.0, 10.0, 17))
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
#>     "bbox": [
#>         100,
#>         -10,
#>         3,
#>         105,
#>         10,
#>         17
#>     ]
#> }

# get bounding box
z <- y %>% feature() %>% bbox_add()
bbox_get(z)
#> [1] 100   0 101   1

## returns NULL if no bounding box
bbox_get(x)
#> NULL
```
