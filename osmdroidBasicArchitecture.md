# osmdroid basic architecture (last updated 2015-06-17)

## Overview

Your app uses a `MapView`.

`MapView` displays `Overlay`'s which are managed by the `OverlayManager`.

The `OverlayManager` initially contains a `TileOverlay`.
Other `Overlay`'s include `MyLocationOverlay`.

`TileOverlay`’s get tiles from a `TileProvider`.

A `TileProvider` has a `TileSource` and a list of `MapTileModule`’s.

`TileSource` defines the type of tile.

`MapTileModule` defines where to get the tile from.

`TileProvider`'s purpose is to return a tile.
If found it will return it, otherwise return null.
Returned tile may be marked as expired.
If null or expired then request from TileSource with callback on success or failure.
The request is State which has a list of TileProvider’s.
On failure try next TileProvider.
On success send a message to invalidate view.
(Note to self: the above is a bit unclear and maybe wrong).

See also https://code.google.com/p/osmdroid/wiki/ModularTileProviderArchitecture

(Note to self: copy everything from this doc and then refer it to here)

Each `MapTileProvider` implementation implements `TileLoader.loadTile`.
