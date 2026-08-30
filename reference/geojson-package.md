# geojson

Classes for GeoJSON to make working with GeoJSON easier

## Package API

GeoJSON objects:

- [`feature`](https://docs.ropensci.org/geojson/reference/feature.md) -
  Feature

- [`featurecollection`](https://docs.ropensci.org/geojson/reference/featurecollection.md) -
  FeatureCollection

- [`geometrycollection`](https://docs.ropensci.org/geojson/reference/geometrycollection.md) -
  GeometryCollection

- [`linestring`](https://docs.ropensci.org/geojson/reference/linestring.md) -
  LineString

- [`multilinestring`](https://docs.ropensci.org/geojson/reference/multilinestring.md) -
  MultiLineString

- [`multipoint`](https://docs.ropensci.org/geojson/reference/multipoint.md) -
  MultiPoint

- [`multipolygon`](https://docs.ropensci.org/geojson/reference/multipolygon.md) -
  MultiPolygon

- [`point`](https://docs.ropensci.org/geojson/reference/point.md) -
  Point

- [`polygon`](https://docs.ropensci.org/geojson/reference/polygon.md) -
  Polygon

The above are assigned two classes. All of them are class **geojson**,
but also have a class name that is **geo** plus the name of the
geometry, e.g., **geopolygon** for polygon.

GeoJSON properties:

- [`properties_add`](https://docs.ropensci.org/geojson/reference/properties.md),
  [`properties_get`](https://docs.ropensci.org/geojson/reference/properties.md) -
  Add or get properties

- [`crs_add`](https://docs.ropensci.org/geojson/reference/crs.md),
  [`crs_get`](https://docs.ropensci.org/geojson/reference/crs.md) - Add
  or get CRS

- [`bbox_add`](https://docs.ropensci.org/geojson/reference/bbox.md),
  [`bbox_get`](https://docs.ropensci.org/geojson/reference/bbox.md) -
  Add or get bounding box

GeoJSON operations:

- [`geo_bbox`](https://docs.ropensci.org/geojson/reference/geo_bbox.md) -
  calculate a bounding box for any GeoJSON object

- [`geo_pretty`](https://docs.ropensci.org/geojson/reference/geo_pretty.md) -
  pretty print any GeoJSON object

- [`geo_type`](https://docs.ropensci.org/geojson/reference/geo_type.md) -
  get the object type for any GeoJSON object

- [`geo_write`](https://docs.ropensci.org/geojson/reference/geo_write.md) -
  easily write any GeoJSON to a file

- More complete GeoJSON operations are provdied in the package geoops

GeoJSON/Geobuf serialization:

- [`from_geobuf`](https://docs.ropensci.org/geojson/reference/geobuf.md) -
  Geobuf to GeoJSON

- [`to_geobuf`](https://docs.ropensci.org/geojson/reference/geobuf.md) -
  GeoJSON to Geobuf

- Check out <https://github.com/mapbox/geobuf> for inormation on the
  Geobuf format

## Coordinate Reference System

According to RFC 7946
(<https://datatracker.ietf.org/doc/html/rfc7946#page-12>) the CRS for
all GeoJSON objects must be WGS-84, equivalent to
`urn:ogc:def:crs:OGC::CRS84`. And lat/long must be in decimal degrees.

Given the above, but considering that GeoJSON blobs exist that have CRS
attributes in them, we provide CRS helpers in this package. But moving
forward these are not likely to be used much.

## Coordinate precision

According to RFC 7946
(<https://datatracker.ietf.org/doc/html/rfc7946#section-11.2>) consider
that 6 decimal places amoutns to ~10 centimeters, a precision well
within that of current GPS sytems. Further, A GeoJSON text containing
many detailed Polygons can be inflated almost by a factor of two by
increasing coordinate precision from 6 to 15 decimal places - so
consider whether it is worth it to have more decimal places.

## Author

Scott Chamberlain, Jeroen Ooms
