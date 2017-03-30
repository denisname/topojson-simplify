# TopoJSON Simplify

Topology-preserving simplification and filtering for TopoJSON. Smaller files, faster rendering!

For an introduction to line simplification:

* https://bost.ocks.org/mike/simplify/
* https://www.jasondavies.com/simplify/

## Installing

If you use NPM, `npm install topojson-simplify`. Otherwise, download the [latest release](https://github.com/topojson/topojson-simplify/releases/latest). You can also load directly from [unpkg](https://unpkg.com). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `topojson` global is exported:

```html
<script src="https://unpkg.com/topojson-client@3"></script>
<script src="https://unpkg.com/topojson-simplify@3"></script>
<script>

topojson.presimplify(topology);

</script>
```

[Try topojson-simplify in your browser.](https://tonicdev.com/npm/topojson-simplify)

# API Reference

<a name="presimplify" href="#presimplify">#</a> topojson.<b>presimplify</b>(<i>topology</i>[, <i>weight</i>]) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/presimplify.js "Source")

Returns a shallow copy of the specified *topology* where each coordinate of each arc is assigned a *z*-value according to the specified *weight* function. If *weight* is not specified, it defaults to [planarTriangleArea](#planarTriangleArea). If the input *topology* is delta-encoded (that is, if a *topology*.transform is present), this transform is removed in the returned output topology.

The returned presimplified topology can be passed to [simplify](#simplify) to remove coordinates below a desired weight threshold.

<a name="simplify" href="#simplify">#</a> topojson.<b>simplify</b>(<i>topology</i>[, <i>minWeight</i>[, <i>weight</i>]]) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/simplify.js "Source")

Returns a shallow copy of the specified *topology*, where every arc coordinate whose *z*-value is lower than *minWeight* is removed; only the *x* and *y* dimensions of the coordinates are preserved in the returned topology. If *minWeight* is not specified, it defaults to [Number.MIN_VALUE](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_VALUE). This method has no effect on Point and MultiPoint geometries.

See [presimplify](#presimplify) to assign *z*-value for each coordinate. See also [toposimplify](#toposimplify).

<a name="quantile" href="#quantile">#</a> topojson.<b>quantile</b>(<i>topology</i>, <i>p</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/quantile.js "Source")

Returns the *p*-quantile of the weighted points in the given [presimplified](#presimplify) *topology*, where *p* is a number in the range [0, 1]. The quantile value is then typically passed as the *minWeight* to [simplify](#simplify). For example, the median weight can be computed using *p* = 0.5, the first quartile at *p* = 0.25, and the third quartile at *p* = 0.75. This implementation uses the [R-7 method](https://en.wikipedia.org/wiki/Quantile#Quantiles_of_a_population), which is the default for the R programming language and Excel.

### Filtering

<a name="filter" href="#filter">#</a> topojson.<b>filter</b>(<i>topology</i>[, <i>filter</i>]) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/filter.js "Source")

…

<a name="filterAttached" href="#filterAttached">#</a> topojson.<b>filterAttached</b>(<i>topology</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/filterAttached.js "Source")

…

<a name="filterWeight" href="#filterWeight">#</a> topojson.<b>filterWeight</b>(<i>topology</i>[, <i>minWeight</i>[, <i>weight</i>]]) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/filterWeight.js "Source")

… If *minWeight* is not specified, it defaults to [Number.MIN_VALUE](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_VALUE). If *weight* is not specified, it defaults to [planarRingArea](#planarRingArea).

<a name="_filter" href="#_filter">#</a> <i>filter</i>(<i>ring</i>, <i>interior</i>)

To filter a topology, you supply a *filter* function to [filter](#filter). The *filter* function is invoked for each ring in the input topology, being passed two arguments: the *ring*, specified as an array of points where each point is a two-element array of numbers, and the *interior* flag. If *interior* is false, the given *ring* is the exterior ring of a polygon; if *interior* is true, the given *ring* is an interior ring (a hole). The *filter* function must then return true if the ring should be preserved, or false if the ring should be removed.

See [filterAttached](#filterAttached) and [filterWeight](#filterWeight) for built-in filter implementations.

### Geometry

<a name="planarRingArea" href="#planarRingArea">#</a> topojson.<b>planarRingArea</b>(<i>ring</i>, <i>interior</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/planar.js#L6 "Source")

…

<a name="planarTriangleArea" href="#planarTriangleArea">#</a> topojson.<b>planarTriangleArea</b>(<i>triangle</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/planar.js#L1 "Source")

…

<a name="sphericalRingArea" href="#sphericalRingArea">#</a> topojson.<b>sphericalRingArea</b>(<i>ring</i>, <i>interior</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/spherical.js#L14 "Source")

…

<a name="sphericalTriangleArea" href="#sphericalTriangleArea">#</a> topojson.<b>sphericalTriangleArea</b>(<i>triangle</i>) [<>](https://github.com/topojson/topojson-simplify/blob/master/src/spherical.js#L43 "Source")

…

## Command Line Reference

### toposimplify

<a name="toposimplify" href="#toposimplify">#</a> <b>toposimplify</b> [<i>options…</i>] [<i>file</i>] [<>](https://github.com/topojson/topojson-simplify/blob/master/bin/toposimplify "Source")

… See also [topojson.simplify](#simplify).

<a name="toposimplify_help" href="#toposimplify_help">#</a> toposimplify <b>-h</b>
<br><a href="#toposimplify_help">#</a> toposimplify <b>--help</b>

Output usage information.

<a name="toposimplify_version" href="#toposimplify_version">#</a> toposimplify <b>-V</b>
<br><a href="#toposimplify_version">#</a> toposimplify <b>--version</b>

Output the version number.

<a name="toposimplify_out" href="#toposimplify_out">#</a> toposimplify <b>-o</b> <i>file</i>
<br><a href="#toposimplify_out">#</a> toposimplify <b>--out</b> <i>file</i>

Specify the output TopoJSON file name. Defaults to “-” for stdout.

<a name="toposimplify_planar_area" href="#toposimplify_planar_area">#</a> toposimplify <b>-p</b> <i>value</i>
<br><a href="#toposimplify_planar_area">#</a> toposimplify <b>--planar-area</b> <i>value</i>

Specify simplification threshold *value* as the minimum planar triangle area, typically in square pixels.

<a name="toposimplify_planar_quantile" href="#toposimplify_planar_quantile">#</a> toposimplify <b>-P</b> <i>value</i>
<br><a href="#toposimplify_planar_quantile">#</a> toposimplify <b>--planar-quantile</b> <i>value</i>

Specify simplification threshold *value* as the minimum quantile of planar triangle areas. The *value* should be in the range [0, 1].

<a name="toposimplify_spherical_area" href="#toposimplify_spherical_area">#</a> toposimplify <b>-s</b> <i>value</i>
<br><a href="#toposimplify_spherical_area">#</a> toposimplify <b>--spherical-area</b> <i>value</i>

Specify simplification threshold *value* as the minimum spherical triangle area ([spherical excess](http://mathworld.wolfram.com/SphericalExcess.html)), in [steradians](https://en.wikipedia.org/wiki/Steradian).

<a name="toposimplify_spherical_quantile" href="#toposimplify_spherical_quantile">#</a> toposimplify <b>-S</b> <i>value</i>
<br><a href="#toposimplify_spherical_quantile">#</a> toposimplify <b>--spherical-quantile</b> <i>value</i>

Specify simplification threshold *value* as the minimum quantile of spherical triangle areas ([spherical excess](http://mathworld.wolfram.com/SphericalExcess.html)). The *value* should be in the range [0, 1].

<a name="toposimplify_filter_detached" href="#toposimplify_filter_detached">#</a> toposimplify <b>-f</b>
<br><a href="#toposimplify_filter_detached">#</a> toposimplify <b>--filter-detached</b>

Remove detached rings that are smaller than the simplification threshold after simplifying.

<a name="toposimplify_filter_all" href="#toposimplify_filter_all">#</a> toposimplify <b>-F</b>
<br><a href="#toposimplify_filter_all">#</a> toposimplify <b>--filter-all</b>

Remove any rings that are smaller than the simplification threshold after simplifying.
