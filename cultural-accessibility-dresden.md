## Research Question
_Does political geography correlate with cultural accessibility?_
## Idea
This project compares two politically contrasting districts in Dresden — 
Gorbitz Süd (highest AfD vote share) and Äußere Neustadt (highest 
left-leaning vote share) — and asks whether spatial inequalities in 
access to cultural venues could potentially be seen as related to political ones.
## Dataset
- District boundaries, theatre/music/dance venues, tram network, 
  bus network, public transport stops  
- Source: City of Dresden, Office for Geodata and Cadastre  
- License: dl-de/by-2-0  
## Method
All steps in QGIS 3.40 (Bratislava) with QNEAT3 plugin.  
CRS throughout: EPSG:25833.

1. Load all datasets from `/data`. Merge tram and bus layers →  
   Vector → Data Management → Merge Vector Layers →  
   output: `transport_network.geojson`  
   Split lines at intersections → Processing Toolbox → Split lines with lines.  
   Snap stops to network → Snap geometries to layer.
2. Create start points — Vector → Geometry Tools → Centroids  
   on district polygons. Select Gorbitz Süd and Äußere Neustadt →  
   output: `start_points.geojson`
3. Shortest path analysis — Processing Toolbox →  
   Shortest Path (Point to Layer) →  
   input: transport network + start points + theatre locations →  
   output: routes per district.
4. Isochrone calculation — QNEAT3 →  
   Iso-Area as Interpolation (from Point) →  
   max distance: 8000m, cell size: 10 →  
   Raster → Contour → Lines to polygons →  
   output: distance zones (1–2km, 2–3km etc.)
5. Styling — Graduated symbology, red tones for Gorbitz Süd,  
   blue tones for Äußere Neustadt, 40% transparency.
## Stack
QGIS · QNEAT3
## Data
All datasets © City of Dresden, dl-de/by-2-0.  
Available at opendata.dresden.de.  
Raw data files not included — download directly from source.

