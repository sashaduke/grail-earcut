# earcut reference fixtures

`earcut_cases.cpp` builds against the vendored mapbox/earcut.hpp 2.2.4 (Abundance's
`ThirdParty/earcut`) and prints `tests/reference.grl`: each polygon as exact binary64
literals (`%.17g`) and the triangle index list the C++ library returns for it. The Grail port
(`src/earcut.grl`) must reproduce every list exactly; the native case `lib-earcut-reference`
runs it.

```sh
clang++ -std=c++17 -O1 -I<path-to-earcut>/include earcut_cases.cpp -o cases
./cases > ../reference.grl
```

The shapes cover the plain ear-clipping path, holes (bridge finding and hole sorting), duplicate
and collinear points, a zero-area ring, a hole touching the outer ring, and polygons above the
80-vertex threshold that switch on z-order hashing.
