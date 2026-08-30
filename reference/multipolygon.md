# multipolygon class

multipolygon class

## Usage

``` r
multipolygon(x)
```

## Arguments

- x:

  input

## Examples

``` r
x <- '{ "type": "MultiPolygon",
"coordinates": [
  [[[102.0, 2.0], [103.0, 2.0], [103.0, 3.0], [102.0, 3.0], [102.0, 2.0]]],
  [[[100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0]],
  [[100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2]]]
  ]
}'
(y <- multipolygon(x))
#> <MultiPolygon> 
#>   no. polygons:  2 
#>   coordinates:  [[[[102.0,2.0],[103.0,2.0],[103.0,3.0],[102.0,3.0],[102.0,2.0]]],[[[10 ... 
geo_type(y)
#> [1] "MultiPolygon"
geo_pretty(y)
#> {
#>     "type": "MultiPolygon",
#>     "coordinates": [
#>         [
#>             [
#>                 [
#>                     102.0,
#>                     2.0
#>                 ],
#>                 [
#>                     103.0,
#>                     2.0
#>                 ],
#>                 [
#>                     103.0,
#>                     3.0
#>                 ],
#>                 [
#>                     102.0,
#>                     3.0
#>                 ],
#>                 [
#>                     102.0,
#>                     2.0
#>                 ]
#>             ]
#>         ],
#>         [
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
#>             ],
#>             [
#>                 [
#>                     100.2,
#>                     0.2
#>                 ],
#>                 [
#>                     100.8,
#>                     0.2
#>                 ],
#>                 [
#>                     100.8,
#>                     0.8
#>                 ],
#>                 [
#>                     100.2,
#>                     0.8
#>                 ],
#>                 [
#>                     100.2,
#>                     0.2
#>                 ]
#>             ]
#>         ]
#>     ]
#> }
#>  
geo_write(y, f <- tempfile(fileext = ".geojson"))
jsonlite::fromJSON(f, FALSE)
#> $type
#> [1] "MultiPolygon"
#> 
#> $coordinates
#> $coordinates[[1]]
#> $coordinates[[1]][[1]]
#> $coordinates[[1]][[1]][[1]]
#> $coordinates[[1]][[1]][[1]][[1]]
#> [1] 102
#> 
#> $coordinates[[1]][[1]][[1]][[2]]
#> [1] 2
#> 
#> 
#> $coordinates[[1]][[1]][[2]]
#> $coordinates[[1]][[1]][[2]][[1]]
#> [1] 103
#> 
#> $coordinates[[1]][[1]][[2]][[2]]
#> [1] 2
#> 
#> 
#> $coordinates[[1]][[1]][[3]]
#> $coordinates[[1]][[1]][[3]][[1]]
#> [1] 103
#> 
#> $coordinates[[1]][[1]][[3]][[2]]
#> [1] 3
#> 
#> 
#> $coordinates[[1]][[1]][[4]]
#> $coordinates[[1]][[1]][[4]][[1]]
#> [1] 102
#> 
#> $coordinates[[1]][[1]][[4]][[2]]
#> [1] 3
#> 
#> 
#> $coordinates[[1]][[1]][[5]]
#> $coordinates[[1]][[1]][[5]][[1]]
#> [1] 102
#> 
#> $coordinates[[1]][[1]][[5]][[2]]
#> [1] 2
#> 
#> 
#> 
#> 
#> $coordinates[[2]]
#> $coordinates[[2]][[1]]
#> $coordinates[[2]][[1]][[1]]
#> $coordinates[[2]][[1]][[1]][[1]]
#> [1] 100
#> 
#> $coordinates[[2]][[1]][[1]][[2]]
#> [1] 0
#> 
#> 
#> $coordinates[[2]][[1]][[2]]
#> $coordinates[[2]][[1]][[2]][[1]]
#> [1] 101
#> 
#> $coordinates[[2]][[1]][[2]][[2]]
#> [1] 0
#> 
#> 
#> $coordinates[[2]][[1]][[3]]
#> $coordinates[[2]][[1]][[3]][[1]]
#> [1] 101
#> 
#> $coordinates[[2]][[1]][[3]][[2]]
#> [1] 1
#> 
#> 
#> $coordinates[[2]][[1]][[4]]
#> $coordinates[[2]][[1]][[4]][[1]]
#> [1] 100
#> 
#> $coordinates[[2]][[1]][[4]][[2]]
#> [1] 1
#> 
#> 
#> $coordinates[[2]][[1]][[5]]
#> $coordinates[[2]][[1]][[5]][[1]]
#> [1] 100
#> 
#> $coordinates[[2]][[1]][[5]][[2]]
#> [1] 0
#> 
#> 
#> 
#> $coordinates[[2]][[2]]
#> $coordinates[[2]][[2]][[1]]
#> $coordinates[[2]][[2]][[1]][[1]]
#> [1] 100.2
#> 
#> $coordinates[[2]][[2]][[1]][[2]]
#> [1] 0.2
#> 
#> 
#> $coordinates[[2]][[2]][[2]]
#> $coordinates[[2]][[2]][[2]][[1]]
#> [1] 100.8
#> 
#> $coordinates[[2]][[2]][[2]][[2]]
#> [1] 0.2
#> 
#> 
#> $coordinates[[2]][[2]][[3]]
#> $coordinates[[2]][[2]][[3]][[1]]
#> [1] 100.8
#> 
#> $coordinates[[2]][[2]][[3]][[2]]
#> [1] 0.8
#> 
#> 
#> $coordinates[[2]][[2]][[4]]
#> $coordinates[[2]][[2]][[4]][[1]]
#> [1] 100.2
#> 
#> $coordinates[[2]][[2]][[4]][[2]]
#> [1] 0.8
#> 
#> 
#> $coordinates[[2]][[2]][[5]]
#> $coordinates[[2]][[2]][[5]][[1]]
#> [1] 100.2
#> 
#> $coordinates[[2]][[2]][[5]][[2]]
#> [1] 0.2
#> 
#> 
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
#> 1     1 <gmltplyg [1]>
#> 2     2 <gmltplyg [1]>
#> 3     3 <gmltplyg [1]>
#> 4     4 <gmltplyg [1]>
#> 5     5 <gmltplyg [1]>
```
