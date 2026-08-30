# linestring class

linestring class

## Usage

``` r
linestring(x)
```

## Arguments

- x:

  input

## Examples

``` r
x <- '{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }'
(y <- linestring(x))
#> <LineString> 
#>   coordinates:  [[100.0,0.0],[101.0,1.0]] 
geo_type(y)
#> [1] "LineString"
geo_pretty(y)
#> {
#>     "type": "LineString",
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
#> [1] "LineString"
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
#> 1     1 <glnstrng [1]>
#> 2     2 <glnstrng [1]>
#> 3     3 <glnstrng [1]>
#> 4     4 <glnstrng [1]>
#> 5     5 <glnstrng [1]>
```
