# multipoint class

multipoint class

## Usage

``` r
multipoint(x)
```

## Arguments

- x:

  input

## Examples

``` r
x <- '{"type": "MultiPoint", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }'
(y <- multipoint(x))
#> <MultiPoint> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
geo_type(y)
#> [1] "MultiPoint"
geo_pretty(y)
#> {
#>     "type": "MultiPoint",
#>     "coordinates": [
#>         [
#>             100.0,
#>             0.0
#>         ],
#>         [
#>             101.0,
#>             1.0
#>         ]
#>     ]
#> }
#>  
geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "MultiPoint"
#> 
#> $coordinates
#> $coordinates[[1]]
#> $coordinates[[1]][[1]]
#> [1] 100
#> 
#> $coordinates[[1]][[2]]
#> [1] 0
#> 
#> 
#> $coordinates[[2]]
#> $coordinates[[2]][[1]]
#> [1] 101
#> 
#> $coordinates[[2]][[2]]
#> [1] 1
#> 
#> 
#> 
unlink(f)

# add to a data.frame
library('tibble')
tibble(a = 1:5, b = list(y))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <gemltpnt [1]>
#> 2     2 <gemltpnt [1]>
#> 3     3 <gemltpnt [1]>
#> 4     4 <gemltpnt [1]>
#> 5     5 <gemltpnt [1]>

# as.geojson coercion
as.geojson(x)
#> <geojson> 
#>   type:  MultiPoint 
#>   points (n): 2 
#>   coordinates: [[100.0,0.0],[101.0,1.0]] 
```
