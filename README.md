-   [Installation](#installation)
-   [Usage](#usage)
-   [Code of Conduct](#code-of-conduct)

<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Build Status](https://travis-ci.org/osmdatar/osmdata.svg?branch=master)](https://travis-ci.org/osmdatar/osmdata) [![Build status](https://ci.appveyor.com/api/projects/status/github/osmdatar/osmdata?svg=true)](https://ci.appveyor.com/project/mpadge/osmdata) [![codecov](https://codecov.io/gh/osmdatar/osmdata/branch/master/graph/badge.svg)](https://codecov.io/gh/osmdatar/osmdata) [![Project Status: WIP](http://www.repostatus.org/badges/0.1.0/wip.svg)](http://www.repostatus.org/#wip) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/osmdata)](http://cran.r-project.org/web/packages/osmdata)

![](./docs/fig/title.png)

`osmdata` is an R package for accessing OpenStreetMap (OSM) data using the [Overpass API](http://wiki.openstreetmap.org/wiki/Overpass_API). The Overpass API (or OSM3S) is a read-only API that serves up custom selected parts of the OSM map data. Map data are returned as [`sp`](https://cran.r-project.org/package=sp) objects.

### Installation

``` r
devtools::install_github("osmdatar/osmdata")
```

Current version:

``` r
library(osmdata)
packageVersion("osmdata")
#> [1] '0.0.0'
```

### Usage

[Overpass API](http://wiki.openstreetmap.org/wiki/Overpass_API) queries can be built from a base query constructed with `opq` followed by `add_feature`. The corresponding OSM objects are then downloaded and converted to `R Simple Features (sf)` objects with `osmdata_sf()` or to `R Spatial (sp)` objects with `osmdata_sp()`. For example,

``` r
q0 <- opq (bbox=c(-0.27,51.47,-0.20,51.50)) # Chiswick Eyot in London, U.K.
q1 <- add_feature (q0, key='name', value="Thames", exact=FALSE)
x <- osmdata_sf (q1)
x
#> Object of class 'osmdata' with:
#>                  $bbox : 51.47,-0.27,51.5,-0.2
#>         $overpass_call : The call submitted to the overpass API
#>             $timestamp : [ Mon Feb 27 10:23:29 2017 ]
#>            $osm_points : 'sf' Simple Features Collection with 21304 points
#>             $osm_lines : 'sf' Simple Features Collection with 1891 linestrings
#>          $osm_polygons : 'sf' Simple Features Collection with 22 polygons
#>        $osm_multilines : 'sf' Simple Features Collection with 5 multilinestrings
#>     $osm_multipolygons : 'sf' Simple Features Collection with 3 multipolygons
```

OSM data can also be downloaded in OSM XML format with `osmdata_xml()` and saved for use with other software.

``` r
osmdata_xml (q1, "data.xml")
```

The `XML` document is returned silently and may be passed directly to `osmdata_sp()` or `osmdata_sf()`

``` r
doc <- osmdata_xml (q1, "data.xml")
x <- osmdata_sf (q1, doc)
```

Or data can be read from a previously downloaded file:

``` r
x <- osmdata_sf (q1, "data.xml")
```

For more details, see the [website](https://osmdatar.github.io/osmdata/)

### Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.
