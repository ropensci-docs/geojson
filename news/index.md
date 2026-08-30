# Changelog

## geojson (development version)

## geojson 0.3.5

CRAN release: 2023-08-08

- Now working in main branch, removed references to old trunk branch.

- Removed geojsonlint and all linting facilities and code.
  [`linting_opts()`](https://docs.ropensci.org/geojson/reference/linting_opts.md)
  is deprecated.

- New maintainer Michael Sumner.

## geojson 0.3.4

CRAN release: 2020-06-23

#### MINOR IMPROVEMENTS

- fixes for test suite: skip package check warnings when geojsonlint not
  available, and skip tests that would use geojsonlint
  ([\#40](https://github.com/ropensci/geojson/issues/40))

## geojson 0.3.2

CRAN release: 2019-01-31

#### BUG FIXES

- fix typo within
  [`ndgeo_read()`](https://docs.ropensci.org/geojson/reference/ndgeo.md)
  ([\#39](https://github.com/ropensci/geojson/issues/39))

## geojson 0.3.0

CRAN release: 2019-01-18

#### NEW FEATURES

- package gains two new functions for working with newline-delimited
  GeoJSON:
  [`ndgeo_write()`](https://docs.ropensci.org/geojson/reference/ndgeo.md)
  and
  [`ndgeo_read()`](https://docs.ropensci.org/geojson/reference/ndgeo.md).
  [`ndgeo_write()`](https://docs.ropensci.org/geojson/reference/ndgeo.md)
  leverages [`writeLines()`](https://rdrr.io/r/base/writeLines.html) to
  write to disk, while
  [`ndgeo_read()`](https://docs.ropensci.org/geojson/reference/ndgeo.md)
  leverages a modified version of
  [`jsonlite::stream_in()`](https://jeroen.r-universe.dev/jsonlite/reference/stream_in.html)
  to stream in line by line.
  [`ndgeo_write()`](https://docs.ropensci.org/geojson/reference/ndgeo.md)
  works only with the geojson package classes `geofeature` and
  `geofeaturecollection`
  ([\#31](https://github.com/ropensci/geojson/issues/31))
  ([\#38](https://github.com/ropensci/geojson/issues/38))
- [`as.geojson()`](https://docs.ropensci.org/geojson/reference/as.geojson.md)
  generic gains a new method for `sf`, see `showMethods('as.geojson')`
  to see methods available. The method is only available if you have
  `sf` installed ([\#30](https://github.com/ropensci/geojson/issues/30))
  thanks [@cpsievert](https://github.com/cpsievert)

#### MINOR IMPROVEMENTS

- add examples of using geobuf capabilities to the README
  ([\#35](https://github.com/ropensci/geojson/issues/35))
- in
  [`as.geojson()`](https://docs.ropensci.org/geojson/reference/as.geojson.md)
  now throw warning message from `jsonlite` when json is invalid to help
  user sort out what’s wrong with their JSON when the input is not valid
  JSON ([\#32](https://github.com/ropensci/geojson/issues/32))
- speed up for an internal method `asc()` to use
  [`stringi::stri_replace_all()`](https://rdrr.io/pkg/stringi/man/stri_replace.html)
  if installed, and if not fall back to using
  [`gsub()`](https://rdrr.io/r/base/grep.html)
- replace usage of
  [`tibble::data_frame()`](https://tibble.tidyverse.org/reference/deprecated.html)
  with
  [`tibble::tibble()`](https://tibble.tidyverse.org/reference/tibble.html)
  throughout package

#### BUG FIXES

- change to `print.geojson()` to not calculate and print the bounding
  box because for very large geojson can take a very long time. Also
  changed to precomputing everything so printing geojson objects is fast
  ([\#36](https://github.com/ropensci/geojson/issues/36))
- fix to
  [`geo_bbox()`](https://docs.ropensci.org/geojson/reference/geo_bbox.md)
  to handle negative coordinates
  ([\#33](https://github.com/ropensci/geojson/issues/33))
  ([\#34](https://github.com/ropensci/geojson/issues/34)) thanks very
  much [@aoles](https://github.com/aoles)

## geojson 0.2.0

CRAN release: 2017-11-08

#### NEW FEATURES

- gains new function `to_geojson` convert GeoJSON character string to
  the approriate GeoJSON class by detecting GeoJSON type automatically.
  this makes some other tasks easier
  ([\#28](https://github.com/ropensci/geojson/issues/28))
  ([\#29](https://github.com/ropensci/geojson/issues/29))

#### MINOR IMPROVEMENTS

- Improve `as.geojson` function to do print summary on all GeoJSON types
  well, not just GeometryCollection and FeatureCollection
  ([\#27](https://github.com/ropensci/geojson/issues/27))

## geojson 0.1.4

CRAN release: 2017-10-24

#### MINOR IMPROVEMENTS

- Changed
  [`properties_add()`](https://docs.ropensci.org/geojson/reference/properties.md)
  to give back the same class object as that given to the function. In
  addition, correctly adds properties to FeatureCollection objects as
  well. ([\#22](https://github.com/ropensci/geojson/issues/22))
- Added properties fxns tests

#### BUG FIXES

- Fixed bug in `print.featurecollection()` that was not calculating and
  printing number of features correctly
  ([\#24](https://github.com/ropensci/geojson/issues/24))

## geojson 0.1.2

CRAN release: 2017-02-28

#### BUG FIXES

- Fixed bug in internal function that checked for existence of a
  Suggested package
  ([\#17](https://github.com/ropensci/geojson/issues/17))

## geojson 0.1.0

CRAN release: 2016-11-16

#### NEW FEATURES

- Released to CRAN.
