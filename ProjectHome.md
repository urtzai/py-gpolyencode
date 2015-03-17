Python port of the Javascript Google Maps polyline encoder from Mark McClure, released under a BSD license. Both a pure python (`gpolyencode`) and a C++ extension (`cgpolyencode`) are implemented, with numerous unit tests.

  * [Google Maps documentation](http://code.google.com/apis/maps/documentation/overlays.html#Encoded_Polylines)
  * [More docs, Javascript encoder, lots of examples](http://facstaff.unca.edu/mcmcclur/GoogleMaps/EncodePolyline/)

## Licensing ##

Copyright (c) 2009, [Koordinates Limited](http://koordinates.com)

Released under the New **BSD License**.

## Requirements ##

  * Python >= 2.4
  * for the C++ extension, a compiler, python headers, C++ standard library, etc
  * to run the tests, SimpleJSON (Python < 2.6) and Nose >= 0.10

## Installing ##

### Pure Python module (`gpolyencode`) ###

```
$ sudo python python/setup.py install
```

If you have the Python `easy_install` utility available, you can also type the following to download and install in one step:

```
$ sudo easy_install gpolyencode
$ sudo easy_install --upgrade gpolyencode    # to force upgrading
```

### C++ extension module module (`cgpolyencode`) ###
```
$ sudo python cpp/setup.py install
```

If you have the Python `easy_install` utility available, you can also type the following to download and install in one step:

```
$ sudo easy_install cgpolyencode
$ sudo easy_install --upgrade cgpolyencode    # to force upgrading
```
## Documentation ##

```
>>> import gpolyencode
>>> encoder = gpolyencode.GPolyEncoder()
# points are a sequence of (longitude,latitude) coordinate pairs
>>> points = ((8.94328,52.29834), (8.93614,52.29767), (8.93301,52.29322), (8.93036,52.28938), (8.97475,52.27014),)
>>> encoder.encode(points)
{'points':'soe~Hovqu@dCrk@xZpR~VpOfwBmtG', 'levels':'PG@IP', 'zoomFactor':2, 'numLevels':18}
```

Once you have your dictionary, passing it through a JSON encoder and adding it to some HTML or Javascript should be a piece of cake. See the [Google Maps API documentation](http://code.google.com/apis/maps/documentation/overlays.html#Encoded_Polylines) for GPolyline and GPolygon, or [Mark's website](http://facstaff.unca.edu/mcmcclur/GoogleMaps/EncodePolyline/) for lots of examples.

The constructor takes several arguments:
  * `num_levels` specifies how many different levels of magnification the polyline will have. (default: 18)
  * `zoom_factor` specifies the change in magnification between those levels. (default: 2)
  * `threshold` indicates the length of a barely visible object at the highest zoom level. (default: 0.00001)
  * `force_endpoints` indicates whether or not the endpoints should be visible at all zoom levels. (default: True)

See [Mark's notes](http://facstaff.unca.edu/mcmcclur/GoogleMaps/EncodePolyline/description.html) for more details on what these parameters mean and how to tweak them. The defaults are sensible for most situations.

The module `cgpolyencode` provides an identical interface to that of the `gpolyencode` module. Use of the `gpolyencode.GPolyEncoder` can be made more efficient (~40 times faster) by using the `cgpolyencode.GPolyEncoder` instead.

## Running the tests ##

The unit tests check compatibility with the original [Javascript class](http://facstaff.unca.edu/mcmcclur/GoogleMaps/EncodePolyline/PolylineEncoder.js) by Mark. There's a range of tests from simple encode-a-point tests through to 150K point lines.

  1. install both the Python & the C++ modules
  1. run:
```
$ python tests/gpolyencode_tests.py -v
```

## Contributing ##

Bug reports, suggestions, feedback, and contributions are all very welcome.

  * Issue Tracker:  http://code.google.com/p/py-gpolyencode/issues/list
  * Email:          robert.coup@koordinates.com