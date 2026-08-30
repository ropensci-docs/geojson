# GeoJSON Linting

GeoJSON Linting

## Usage

``` r
linting_opts(
  lint = FALSE,
  method = "hint",
  error = FALSE,
  suppress_pkgcheck_warnings = FALSE
)
```

## Arguments

- lint:

  (logical) lint geojson or not. Default: `FALSE`

- method:

  (character) method to use:

  - hint - uses `geojsonlint::geojson_hint()`

  - lint - uses `geojsonlint::geojson_lint()`

  - validate - uses `geojsonlint::geojson_validate()`

- error:

  (logical) Throw an error on parse failure? If `TRUE`, then function
  returns `TRUE` on success, and stop with the error message on error.
  Default: `FALSE`

- suppress_pkgcheck_warnings:

  (logical) Suppress warning when `geojsonlint` is not installed?
  Default: `FALSE`

## Details

linting_opts was deprecated in 0.3.5
