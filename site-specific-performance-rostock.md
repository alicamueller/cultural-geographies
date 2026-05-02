## Research Question
_Which park areas in Rostock are suitable for a site-specific performance?_
## Dataset
All datasets from City of Rostock Open Data Portal (2025):
- Park areas, public transport stops, cultural facilities 
  (museums, theatres), public toilets, noise exposure layers 
  (Straßenverkehrslärm 2022, Industrie- und Hafenlärm 2022)
## Method
All steps in QGIS 3.36. CRS throughout: ETRS89 / UTM Zone 33N (EPSG:25833).  
Reproject all layers if necessary: right-click → Export → Save Features As → CRS: EPSG:25833.

1. **Noise exclusion** — Merge noise layers → Processing Toolbox → 
   Merge Vector Layers. Remove noisy areas → Vector → Geoprocessing → 
   Difference (input: park areas, overlay: noise layer) → 
   output: `parks_quiet`
2. **Accessibility** — Buffer public transport stops 500m → 
   Vector → Geoprocessing → Buffer. Intersect with parks → 
   output: `parks_accessible`
3. **Cultural proximity** — Merge museums and theatres → Buffer 1000m → 
   Intersect with parks → output: `parks_cultural`
4. **Infrastructure** — Count toilets per park → 
   Vector Analysis → Count Points in Polygon. 
   Add binary field via Field Calculator:  
   `CASE WHEN "point_count" > 0 THEN 1 ELSE 0 END` → 
   output: `parks_with_toilets`
5. **Combine criteria** — Sequential intersection:  
   `parks_quiet ∩ parks_accessible ∩ parks_cultural ∩ parks_with_toilets` → 
   output: `parks_final`
6. **Geometry cleanup** — Multipart to Singleparts → 
   Calculate area: Field Calculator → `area_m2 = $area` → 
   Filter: `"area_m2" >= 100` → export selected features.
## Stack
QGIS
## Data
© City of Rostock Open Data Portal (2025).  
Basemap © OpenStreetMap contributors, © CARTO.  
Raw data files not included — download directly from source. 

