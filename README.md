# Leaflet.Circle-sector

Plugin for [Leaflet](http://leafletjs.com) adding sector (pie-shaped part of a circle) drawing capability to [`L.Circle`](http://leafletjs.com/reference-1.0.2.html#circle).

Based on [jieter / Leaflet-semicircle](https://github.com/jieter/Leaflet-semicircle).

Compatible with Leaflet version 1.0 (tested with 1.0.2), **not** compatible with version 0.x.

See [demo](https://kluizeberg.github.io/Leaflet.Circle-sector/demo.html).

## Installation and usage

1. load `leaflet.js`
2. load `leaflet.circle-sector.js`
3. create `L.Circle` instance(s):
```javascript
var sector = L.circle([50, 5], {
	radius: 1234,
	startAngle: 60,
	endAngle: 120,
}).addTo(map);
```

or:
```javascript
var sector = L.circle([50, 5], {radius: 1234}).setAngles(60, 120).addTo(map);
```

or:
```javascript
var sector = L.circle([50, 5], {radius: 1234}).setSector(90, 60).addTo(map);
```

See also [`demo.html`](demo.html).

## API

This plugin alters Leaflet's class `L.Circle` and adds helper methods to class `L.CRS.Earth` as well as private methods to renderer classes `L.Canvas` and `L.SVG`.

Angles are in degrees, clockwise from North.

### [`L.Circle`](http://leafletjs.com/reference-1.0.2.html#circle) *additions*

| Option | Type | Default | Description |
| :----- | :--- | :------ | :---------- |
| `startAngle` | `Number` | `0` | Start angle of sector. |
| `endAngle` | `Number` | `360` | End angle of sector. |

Pragmatic assumption: `startAngle <= endAngle`. When `endAngle - startAngle >= 360`, a full (normal) circle is drawn.

| Function | Returns | Description |
| :------- | :------ | :---------- |
| `contains(<LatLng> latLng)` | `Boolean` | Returns `true` if the circle (sector) contains the given point. |
| `getBounds()` | `LatLngBounds` | Returns the `LatLngBounds` of the circle (sector). |
| `setAngles(<Number> start, <Number> end)` | `this` | Sets the start and end angles of a circle (sector), non-numeric values are ignored. |
| `setSector(<Number> direction, <Number> centralAngle?)` | `this` | Alternative angle setter through main direction and central angle; previously set central angle is retained if omitted. |

### [`L.CRS.Earth`](http://leafletjs.com/reference-1.0.2.html#crs-l-crs-earth) *additions*

**Note**: these methods require true `LatLng`s.

| Function | Returns | Description |
| :------- | :------ | :---------- |
| `bearing(<LatLng> latLng1, <LatLng> latLng2)` | `Number` | Returns initial bearing (degrees normalized to 0-360) on great circle path from latLng1 to latLng2. |
| `destination(<LatLng> latLng, <Number> bearing, <Number> distance)` | `LatLng` | Returns destination point given distance (meters) and bearing (degrees) from latLng. |
