# Geojson class

Geojson class

## Usage

``` r
as.geojson(x)

# S4 method for class 'json'
as.geojson(x)

# S4 method for class 'geojson'
as.geojson(x)

# S4 method for class 'character'
as.geojson(x)

# S4 method for class 'SpatialPointsDataFrame'
as.geojson(x)

# S4 method for class 'SpatialPoints'
as.geojson(x)

# S4 method for class 'SpatialLinesDataFrame'
as.geojson(x)

# S4 method for class 'SpatialLines'
as.geojson(x)

# S4 method for class 'SpatialPolygonsDataFrame'
as.geojson(x)

# S4 method for class 'SpatialPolygons'
as.geojson(x)
```

## Arguments

- x:

  input, an object of class character, json, SpatialPoints,
  SpatialPointsDataFrame, SpatialLines, SpatialLinesDataFrame,
  SpatialPolygons, or SpatialPolygonsDataFrame

## Value

an object of class geojson/json

## Details

The `print.geojson` method prints the geojson geometry type, the
bounding box, number of features (if applicable), and the geometries and
their lengths

## Examples

``` r
# character
as.geojson(geojson_data$featurecollection_point)
#> Loading required namespace: stringi
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 1 
#>   features (geometry / length) [first 5]:
#>     Point / 2 
as.geojson(geojson_data$polygons_average)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     Polygon / 1
#>     Polygon / 1 
as.geojson(geojson_data$polygons_aggregate)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     Polygon / 1
#>     Polygon / 1 
as.geojson(geojson_data$points_count)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2 

# sp classes

## SpatialPoints
library(sp)
x <- c(1,2,3,4,5)
y <- c(3,2,5,1,4)
s <- SpatialPoints(cbind(x,y))
as.geojson(s)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 5 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2
#>     Point / 2
#>     Point / 2 

## SpatialPointsDataFrame
s <- SpatialPointsDataFrame(cbind(x,y), mtcars[1:5,])
as.geojson(s)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 5 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2
#>     Point / 2
#>     Point / 2 

## SpatialLines
L1 <- Line(cbind(c(1,2,3), c(3,2,2)))
L2 <- Line(cbind(c(1.05,2.05,3.05), c(3.05,2.05,2.05)))
L3 <- Line(cbind(c(1,2,3),c(1,1.5,1)))
Ls1 <- Lines(list(L1), ID = "a")
Ls2 <- Lines(list(L2, L3), ID = "b")
sl1 <- SpatialLines(list(Ls1))
as.geojson(sl1)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 1 
#>   features (geometry / length) [first 5]:
#>     MultiLineString / 1 

## SpatialLinesDataFrame
sl12 <- SpatialLines(list(Ls1, Ls2))
dat <- data.frame(X = c("Blue", "Green"),
                  Y = c("Train", "Plane"),
                  Z = c("Road", "River"), row.names = c("a", "b"))
sldf <- SpatialLinesDataFrame(sl12, dat)
as.geojson(sldf)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     MultiLineString / 1
#>     MultiLineString / 2 

## SpatialPolygons
poly1 <- Polygons(list(Polygon(cbind(c(-100,-90,-85,-100),
   c(40,50,45,40)))), "1")
poly2 <- Polygons(list(Polygon(cbind(c(-90,-80,-75,-90),
   c(30,40,35,30)))), "2")
sp_poly <- SpatialPolygons(list(poly1, poly2), 1:2)
as.geojson(sp_poly)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     Polygon / 1
#>     Polygon / 1 

## SpatialPolygonsDataFrame
sp_polydf <- as(sp_poly, "SpatialPolygonsDataFrame")
as.geojson(sp_polydf)
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 2 
#>   features (geometry / length) [first 5]:
#>     Polygon / 1
#>     Polygon / 1 

## sf objects
if (requireNamespace('sf')) {
  nc <- sf::st_read(system.file("shape/nc.shp", package = "sf"), quiet = TRUE)
  as.geojson(nc)
}
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 100 
#>   features (geometry / length) [first 5]:
#>     Polygon / 1
#>     Polygon / 1
#>     Polygon / 1
#>     Polygon / 3
#>     Polygon / 1 
```
