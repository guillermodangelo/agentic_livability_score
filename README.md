# agentic_livability_score


https://courses.spatialthoughts.com/agentic-coding-geospatial.html#assignment

Since OSM for apartment buildings is not complete for the country of Uruguay, I preferred using building footprints extracts collected by VIDA. I know these are just footprints, but I consider this a better source than a scarcely populated layer of apartments buildings.

Building footprints for Uruguay: https://source.coop/vida/google-microsoft-open-buildings/geoparquet/by_country/country_iso=URY

Area of interest (AOI): restric all analysis to the AOI defined in aoi.gpkg


## Livability score

THe livability score presented is experimental, and adapted to the restrictions in the data

### Key aspects

Closeness to the shoreline: since is a strong cultural value in my country and specifically in this city, this is considered as relevant.


### 1st prompt

Generate a Jupyter Notebook for downloading all the building footprint from URY,
and filter them by the AOI, saving a
geopackage with only the buildings that are within the AOI. Add another cell that filters all building less than 15 sq meters and rerun the notebook