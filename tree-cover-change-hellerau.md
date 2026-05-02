## Research Question
_How has tree cover changed in Hellerau — Germany's first garden city — 
between 2005 and 2022?_
## Dataset
- Digital Orthophotos (DOP) 2005 and 2021–2022  
- Source: GeoSN — Geoportal Sachsenatlas  
## Method
All steps in QGIS 3.40 (Bratislava) and YOLOv9.  
CRS throughout: ETRS89 / UTM Zone 33N (EPSG:25833).

1. **Tree detection** — Run YOLOv9 on DOP 2005 and DOP 2022 separately.  
   Convert bounding box output to vector polygons →  
   output: `Trees_2005.shp`, `Trees_2022.shp`  
   Manual refinement in QGIS: remove false detections (cars, shadows, roofs),  
   add missing trees, ensure consistency between datasets.
2. **Tree loss** — Vector → Geoprocessing → Difference  
   (input: Trees_2005, overlay: Trees_2022) → output: `Lost_Trees`
3. **Tree gain** — Vector → Geoprocessing → Difference  
   (input: Trees_2022, overlay: Trees_2005) → output: `New_Trees`
4. **Persistent trees** — Vector → Geoprocessing → Intersection  
   (input: Trees_2005, overlay: Trees_2022) → output: `Unchanged_Trees`

Note: Minor overlaps between loss and gain layers result from 
tree crown growth and shadow effects between the two time steps.
## Stack
QGIS · YOLOv9
## Data
Digital Orthophotos (DOP 2005 & DOP 2021–2022) © GeoSN — Geoportal Sachsenatlas.  
Raw orthophotos not included due to file size —  download directly from souce.