# polygon class

polygon class

## Usage

``` r
polygon(x)
```

## Arguments

- x:

  input

## Examples

``` r
x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [100.0, 1.0], [101.0, 1.0], [101.0, 0.0], [100.0, 0.0] ]
  ]
}'
(y <- polygon(x))
#> <Polygon> 
#>   no. lines:  1 
#>   no. holes:  0 
#>   no. nodes / line:  5 
#>   coordinates:  [[[100.0,0.0],[100.0,1.0],[101.0,1.0],[101.0,0.0],[100.0,0.0]]] 
y[1]
#> [1] "{ \"type\": \"Polygon\",\n\"coordinates\": [\n  [ [100.0, 0.0], [100.0, 1.0], [101.0, 1.0], [101.0, 0.0], [100.0, 0.0] ]\n  ]\n}"
geo_type(y)
#> [1] "Polygon"
geo_pretty(y)
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
geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "Polygon"
#> 
#> $coordinates
#> $coordinates[[1]]
#> $coordinates[[1]][[1]]
#> $coordinates[[1]][[1]][[1]]
#> [1] 100
#> 
#> $coordinates[[1]][[1]][[2]]
#> [1] 0
#> 
#> 
#> $coordinates[[1]][[2]]
#> $coordinates[[1]][[2]][[1]]
#> [1] 100
#> 
#> $coordinates[[1]][[2]][[2]]
#> [1] 1
#> 
#> 
#> $coordinates[[1]][[3]]
#> $coordinates[[1]][[3]][[1]]
#> [1] 101
#> 
#> $coordinates[[1]][[3]][[2]]
#> [1] 1
#> 
#> 
#> $coordinates[[1]][[4]]
#> $coordinates[[1]][[4]][[1]]
#> [1] 101
#> 
#> $coordinates[[1]][[4]][[2]]
#> [1] 0
#> 
#> 
#> $coordinates[[1]][[5]]
#> $coordinates[[1]][[5]][[1]]
#> [1] 100
#> 
#> $coordinates[[1]][[5]][[2]]
#> [1] 0
#> 
#> 
#> 
#> 
unlink(f)

x <- '{ "type": "Polygon",
"coordinates": [
  [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ],
  [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ]
  ]
}'
(y <- polygon(x))
#> <Polygon> 
#>   no. lines:  2 
#>   no. holes:  1 
#>   no. nodes / line:  5, 5 
#>   coordinates:  [[[100.0,0.0],[101.0,0.0],[101.0,1.0],[100.0,1.0],[100.0,0.0]],[[100.2 ... 
y[1]
#> [1] "{ \"type\": \"Polygon\",\n\"coordinates\": [\n  [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ],\n  [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ]\n  ]\n}"
geo_type(y)
#> [1] "Polygon"
geo_pretty(y)
#> {
#>     "type": "Polygon",
#>     "coordinates": [
#>         [
#>             [
#>                 100.0,
#>                 0.0
#>             ],
#>             [
#>                 101.0,
#>                 0.0
#>             ],
#>             [
#>                 101.0,
#>                 1.0
#>             ],
#>             [
#>                 100.0,
#>                 1.0
#>             ],
#>             [
#>                 100.0,
#>                 0.0
#>             ]
#>         ],
#>         [
#>             [
#>                 100.2,
#>                 0.2
#>             ],
#>             [
#>                 100.8,
#>                 0.2
#>             ],
#>             [
#>                 100.8,
#>                 0.8
#>             ],
#>             [
#>                 100.2,
#>                 0.8
#>             ],
#>             [
#>                 100.2,
#>                 0.2
#>             ]
#>         ]
#>     ]
#> }
#>  

# add to a data.frame
library('tibble')
tibble(a = 1:5, b = list(y))
#> # A tibble: 5 × 2
#>       a b             
#>   <int> <list>        
#> 1     1 <geoplygn [1]>
#> 2     2 <geoplygn [1]>
#> 3     3 <geoplygn [1]>
#> 4     4 <geoplygn [1]>
#> 5     5 <geoplygn [1]>
```
