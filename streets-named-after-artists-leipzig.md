## Research Question
_Which districts of Leipzig have the highest concentration of streets 
named after artists?_
## Dataset
- Street register (Straßenverzeichnis Leipzig) — City of Leipzig, XML, 3,000+ entries  
- District boundaries — Open Data Leipzig  
- Artist-named streets identified: 387  
## Method
All steps in QGIS 3.40 (Bratislava).
1. Download street register XML. Import into Excel. Extract columns: street name, district (Ortsteil), description text.
2. Filter description column using keyword search (case-insensitive) for:  
   `artist, painter, composer, writer, musician, poet, actor, sculptor, architect, singer`  
   Mark rows containing at least one keyword. Result: 387 artist-named streets.
3. Aggregate by district — count artist-named streets per city part. Export as CSV with columns:  
   `district | artist_street_count`
4. Load district shapefile (`geodaten-ortsteile-leipzig`) and CSV into QGIS via  
   Layer → Add Vector Layer and Layer → Add Delimited Text Layer (no geometry).
5. Join layers — Layer Properties → Joins → join field: district name →  
   target field: district name in shapefile.
6. Choropleth map — Layer Properties → Symbology → Graduated →  
   value: `artist_street_count` → Equal intervals → 5 classes → light to dark purple.  
   Districts with count 0: grey.
## Stack
QGIS · Excel
## Data
Street register © City of Leipzig.  
District boundaries © Open Data Leipzig.  
Raw data files not included — download directly from the sources above.

