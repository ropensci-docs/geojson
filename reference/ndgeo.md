# Read and write newline-delimited GeoJSON (GeoJSON text sequences)

There are various flavors of newline-delimited GeoJSON, all of which we
aim to handle here. See Details for more.

## Usage

``` r
ndgeo_write(x, file, sep = "\n")

# Default S3 method
ndgeo_write(x, file, sep = "\n")

# S3 method for class 'geofeaturecollection'
ndgeo_write(x, file, sep = "\n")

# S3 method for class 'geofeature'
ndgeo_write(x, file, sep = "\n")

ndgeo_read(txt, pagesize = 500, verbose = TRUE)
```

## Arguments

- x:

  input, an object of class `geojson`

- file:

  (character) a file. not a connection. required.

- sep:

  (character) a character separator to use in
  [`writeLines()`](https://rdrr.io/r/base/writeLines.html)

- txt:

  text, a file, or a url. required.

- pagesize:

  (integer) number of lines to read/write from/to the connection per
  iteration

- verbose:

  (logical) print messages. default: `TRUE`

## Value

a `geojson` class object

## Details

- `ndgeo_write`: writes geojson package types as newline-delimited
  GeoJSON to a file

- `ndgeo_read`: reads newline-delimited GeoJSON from a string, file, or
  URL into the appropriate geojson type

As an alternative to `ndgeo_read`, you can simply use
[`jsonlite::stream_in()`](https://jeroen.r-universe.dev/jsonlite/reference/stream_in.html)
to convert newline-delimited GeoJSON to a data.frame

## Note

**IMPORTANT**: `ngeo_read` for now only handles lines of geojson in your
file that are either features or geometry objects (e.g., point,
multipoint, polygon, multipolygon, linestring, multilinestring)

## References

Newline-delimited JSON has a few flavors. The only difference between
ndjson <http://ndjson.org/> and JSON Lines <https://jsonlines.org/> I
can tell is that the former requires UTF-8 encoding, while the latter
does not.

GeoJSON text sequences has a specification found at
<https://datatracker.ietf.org/doc/html/rfc8142>. The spec states that:

- a GeoJSON text sequence is any number of GeoJSON RFC7946 texts

- each line encoded in UTF-8 RFC3629

- each line preceded by one ASCII RFC20 record separator (RS; "0x1e")
  character

- each line followed by a line feed (LF)

- each JSON text MUST contain a single GeoJSON object as defined in
  RFC7946

See also the GeoJSON specification
<https://datatracker.ietf.org/doc/html/rfc7946>

## Examples

``` r
# featurecollection
## write
file <- system.file("examples", 'featurecollection2.geojson',
  package = "geojson")
str <- paste0(readLines(file), collapse = " ")
(x <- featurecollection(str))
#> <FeatureCollection> 
#>   type:  FeatureCollection 
#>   no. features:  3 
#>   features (1st 5):  Point, Point, Point 
outfile <- tempfile(fileext = ".geojson")
ndgeo_write(x, outfile)
readLines(outfile)
#> [1] "{\"type\":\"Feature\",\"id\":0,\"properties\":{\"NOME\":\"Sec de segunrança\",\"URL\":\"http://www.theatermania.com/new-york/theaters/45th-street-theatre_2278/\",\"ADDRESS1\":\"354 West 45th Street\",\"CIDADE\":\"Goiânia\",\"CEP\":74250010},\"geometry\":{\"type\":\"Point\",\"coordinates\":[-49.256240,-16.689612]}}"               
#> [2] "{\"type\":\"Feature\",\"id\":1,\"properties\":{\"NOME\":\"Teste\",\"URL\":\"http://www.bestofoffbroadway.com/theaters/47streettheatre.html\",\"ADDRESS1\":\"304 West 47th Street\",\"CIDADE\":\"New York\",\"ZIP\":74250010},\"geometry\":{\"type\":\"Point\",\"coordinates\":[-49.276240,-16.655612]}}"                                   
#> [3] "{\"type\":\"Feature\",\"id\":3,\"properties\":{\"NOME\":\"Delacorte Theater\",\"URL\":\"http://www.centralpark.com/pages/attractions/delacorte-theatre.html\",\"ADDRESS1\":\"Central Park - Mid-Park at 80th Street\",\"CIDADE\":\"New York\",\"ZIP\":74250010},\"geometry\":{\"type\":\"Point\",\"coordinates\":[-49.277263,-16.679057]}}"
jsonlite::stream_in(file(outfile))
#> opening file input connection.
#>  Found 3 records... Imported 3 records. Simplifying...
#> closing file input connection.
#>      type id   properties.NOME
#> 1 Feature  0 Sec de segunrança
#> 2 Feature  1             Teste
#> 3 Feature  3 Delacorte Theater
#>                                                            properties.URL
#> 1 http://www.theatermania.com/new-york/theaters/45th-street-theatre_2278/
#> 2          http://www.bestofoffbroadway.com/theaters/47streettheatre.html
#> 3     http://www.centralpark.com/pages/attractions/delacorte-theatre.html
#>                      properties.ADDRESS1 properties.CIDADE properties.CEP
#> 1                   354 West 45th Street           Goiânia       74250010
#> 2                   304 West 47th Street          New York             NA
#> 3 Central Park - Mid-Park at 80th Street          New York             NA
#>   properties.ZIP geometry.type geometry.coordinates
#> 1             NA         Point -49.25624, -16.68961
#> 2       74250010         Point -49.27624, -16.65561
#> 3       74250010         Point -49.27726, -16.67906
## read
ndgeo_read(outfile)
#> opening file input connection.
#>  Found 3 records...
#> closing file input connection.
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 3 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2 
unlink(outfile)

# read from an existing file
## GeoJSON objects all of same type: Feature
file <- system.file("examples", 'ndgeojson1.json', package = "geojson")
ndgeo_read(file)
#> opening file input connection.
#>  Found 3 records...
#> closing file input connection.
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 3 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2 
## GeoJSON objects all of same type: Point
file <- system.file("examples", 'ndgeojson2.json', package = "geojson")
ndgeo_read(file)
#> opening file input connection.
#>  Found 3 records...
#> closing file input connection.
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 3 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2 
## GeoJSON objects of mixed type: Point, and Feature
file <- system.file("examples", 'ndgeojson3.json', package = "geojson")
ndgeo_read(file)
#> opening file input connection.
#>  Found 3 records...
#> closing file input connection.
#> <geojson> 
#>   type:  FeatureCollection 
#>   features (n): 3 
#>   features (geometry / length) [first 5]:
#>     Point / 2
#>     Point / 2
#>     Point / 2 

if (FALSE) { # \dontrun{
# read from a file
url <- "https://raw.githubusercontent.com/ropensci/geojson/main/inst/examples/ndgeojson1.json"
f <- tempfile(fileext = ".geojsonl")
download.file(url, f)
x <- ndgeo_read(f)
x
unlink(f)

# read from a URL
url <- "https://raw.githubusercontent.com/ropensci/geojson/main/inst/examples/ndgeojson1.json"
x <- ndgeo_read(url)
x

# geojson text sequences from file
file <- system.file("examples", 'featurecollection2.geojson',
  package = "geojson")
str <- paste0(readLines(file), collapse = " ")
x <- featurecollection(str)
outfile <- tempfile(fileext = ".geojson")
ndgeo_write(x, outfile, sep = "\u001e\n")
con <- file(outfile)
readLines(con)
close(con)
ndgeo_read(outfile)
unlink(outfile)
} # }
```
