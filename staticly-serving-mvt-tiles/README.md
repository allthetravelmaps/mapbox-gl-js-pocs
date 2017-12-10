# Mapbox GL JS & Staticly Serving MVT Tiles POC

A POC demostating how to serve mvt map tiles from a static directory.

Check it out live [here](https://allthetravelmaps.github.io/mapbox-gl-js-pocs/staticly-serving-mvt-tiles/).

## Note: Compressed tiles

Tiles extracted from a `.mbtiles` archive are commonly gzip compressed (though their `.pbf` filename suffix suggests otherwise). To serve compressed tiles to the mapbox-gl sdk, the `Content-Type` and `Content-Encoding` http headers must be set correctly. If they're not set correctly, the mapbox-gl sdk will error out with a `Unimplemented type: 3`. Note that the github.io webserver automatically correctly sets the `Content-Encoding` header, but (understandably) just guesses at the `Content-Type` header and gets it wrong. As such, to make this POC work via the github.io webserver, this POC only contains uncompressed tiles.

If [protoc](https://github.com/google/protobuf) is able to decode your tiles, that means they're uncompressed valid protocol buffers. Ex:

```shell
# errors out if tile is compressed, or otherwise an invalid protobuf file
cat 0.pbf | protoc --decode_raw | head
```

[These instructions](https://github.com/klokantech/vector-tiles-sample/tree/v1.0#host-the-vector-tiles-without-any-server-at-all) show how to go from an `.mbtiles` file to directory tree of uncompressed tiles. For unpacking the `.mbtiles` file, [tile-join](https://github.com/mapbox/tippecanoe/tree/v1.8.1#tile-join) appears to be a better-maintained alternative to [mb-util](https://github.com/mapbox/mbutil).

For the tileset I'm currently working with, gzip compression cuts the total size down by 38% (3.6 GB -> 2.2 GB).
