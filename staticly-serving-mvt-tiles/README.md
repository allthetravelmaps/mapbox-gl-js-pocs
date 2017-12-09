# Mapbox GL JS & Staticly Serving MVT Tiles POC

A POC demostating how to serve mvt map tiles from a static directory.

Check it out live [here](https://allthetravelmaps.github.io/mapbox-gl-js-pocs/staticly-serving-mvt-tiles/).

## Note: Compressed tiles

Tiles extracted from a `.mbtiles` archive are commonly `deflate` compressed. If you're going to serve those directly, be careful about setting the http `Content-Type` and `Content-Encoding` headers correctly. If they're not set correctly, the mapbox-gl sdk will error out with a `Unimplemented type: 3`. Note that the github.io webserver does not set these both correctly. As such, this POC only contains uncompressed tiles.

You can check to see if your tiles are compressed or not like so:

```shell
# either errors out (if compressed) or outputs a semi-readable protobuf structure
cat 0.pbf | protoc --decode_raw
```

[These instructions](https://github.com/klokantech/vector-tiles-sample/tree/v1.0#host-the-vector-tiles-without-any-server-at-all) show how to uncompress a directory tree of DEFLATE compressed tiles. For unpacking a .mbtiles file, [tile-join](https://github.com/mapbox/tippecanoe/tree/v1.8.1#tile-join) is a good alternative to [mb-util](https://github.com/mapbox/mbutil).

For the full tileset I'm working with, compressing with deflate cuts the total size down by 38% (3.6 GB -> 2.2 GB).
