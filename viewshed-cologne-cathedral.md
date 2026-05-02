## Research Question
_Which cultural institutions are visible from Cologne Cathedral?_
## Inspiration
Inspired by the pandemic's enforced invisibility of cultural life, and by the work of Christo and Jeanne-Claude, whose wrappings ask what it means to see — or not to see — a cultural institution.
## Dataset
Digital Elevation Model DGM1 (1m resolution) — Geobasis NRW (2022) Cultural institutions (museums, theatres) — OpenStreetMap via QuickOSM Observation point: Cologne Cathedral (356410, 5645260, EPSG:25832)
## Method
All steps in QGIS 3.40 (Bratislava) with GRASS GIS tools. CRS throughout: ETRS89 / UTM Zone 32N (EPSG:25832).

1. Download DGM1 tiles covering Cologne city centre from Geobasis NRW. Merge via Raster → Miscellaneous → Merge → output: `dgm_merged.tif`
2. Run GRASS r.viewshed — input: `dgm_merged.tif`, observer coordinates: 356410 / 5645260, observer height: 157m, target height: 2m, max distance: 500m, earth curvature and atmospheric refraction enabled (coefficient: 0.13)
3. Extract visible area — Raster Calculator: `"viewshed@1" = 1` → Polygonize → filter by `DN = 1` → output: `viewshed_visible.shp`
4. Load OSM data via QuickOSM: `tourism=museum` and `amenity=theatre`, point geometries only, around coordinates 50.9413 / 6.9583, 500m radius. Merge layers → output: `kulturorte_merged.shp`
5. Identify visible institutions — Vector → Extract by Location, intersect with `viewshed_visible.shp`
## Stack
QGIS · GRASS r.viewshed · QuickOSM
## Data
DGM1 © Geobasis NRW (2022). OSM © OpenStreetMap contributors. Raw raster files not included due to file size — download DGM1 tiles directly from Geobasis NRW.

