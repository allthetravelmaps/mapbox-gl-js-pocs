# Mapbox GL JS & Altering a Style dynamically POC

A POC to verify an existing style can be changed on-the-fly and the map will redraw.

It appears the map engine isn't automagically watching the style object for changes. You read out the whole style object, make your changes, then send the whole updated object back to the map engine.

Hopefully the map engine is being smart about what it chooses to redraw or not on the page based on a diff between the previous style and the new one.

Check it out live [here](https://allthetravelmaps.github.io/mapbox-gl-js-pocs/alter-style-dynamically/).
