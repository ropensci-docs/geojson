# Convert GeoJSON character string to approriate GeoJSON class

Automatically detects and adds the class

## Usage

``` r
to_geojson(x)
```

## Arguments

- x:

  GeoJSON character string

## Examples

``` r
mp <- '{"type":"MultiPoint","coordinates":[[100,0],[101,1]]}'
to_geojson(mp)
#> <MultiPoint> 
#>   coordinates:  [[100,0],[101,1]] 

ft <- '{"type":"Feature","properties":{"a":"b"},
"geometry":{"type": "MultiPoint","coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}}'
to_geojson(mp)
#> <MultiPoint> 
#>   coordinates:  [[100,0],[101,1]] 

fc <- '{"type":"FeatureCollection","features":[{"type":"Feature","properties":{"a":"b"},
"geometry":{"type": "MultiPoint","coordinates": [ [100.0, 0.0], [101.0, 1.0] ]}}]}'
to_geojson(fc)
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  1 
#>   features (1st 5):  MultiPoint 
```
