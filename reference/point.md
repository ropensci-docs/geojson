# point class

point class

## Usage

``` r
point(x)
```

## Arguments

- x:

  input

## Examples

``` r
x <- '{ "type": "Point", "coordinates": [100.0, 0.0] }'
(y <- point(x))
#> <Point> 
#>   coordinates:  [100.0,0.0] 
geo_type(y)
#> [1] "Point"
geo_pretty(y)
#> {
#>     "type": "Point",
#>     "coordinates": [
#>         100.0,
#>         0.0
#>     ]
#> }
#>  
geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "Point"
#> 
#> $coordinates
#> $coordinates[[1]]
#> [1] 100
#> 
#> $coordinates[[2]]
#> [1] 0
#> 
#> 
unlink(f)

# add to a data.frame
library('tibble')
tibble(a = 1:5, b = list(y))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <geopoint [1]>
#> 2     2 <geopoint [1]>
#> 3     3 <geopoint [1]>
#> 4     4 <geopoint [1]>
#> 5     5 <geopoint [1]>

# as.geojson coercion
as.geojson(x)
#> <geojson> 
#>   type:  Point 
#>   points (n): 2 
#>   coordinates: [100.0,0.0] 
```
