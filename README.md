# agentic_livability_score


https://courses.spatialthoughts.com/agentic-coding-geospatial.html#assignment

Since OSM for apartment buildings is not complete for the country of Uruguay, I preferred using building footprints extracts collected by VIDA. I know these are just footprints, but I consider this a better source than a scarcely populated layer of apartments buildings.

Building footprints for Uruguay: https://source.coop/vida/google-microsoft-open-buildings/geoparquet/by_country/country_iso=URY

Area of interest (AOI): restrict all analysis to the AOI defined in aoi.gpkg


## Livability score

THe livability score presented is experimental, and adapted to the restrictions in the data

### Key aspects

Closeness to the shoreline: since is a strong cultural value in my country and specifically in this city, this is considered as relevant.


### 1st prompt

Generate a Jupyter Notebook for downloading all the building footprint from URY,
and filter them by the AOI, saving a
geopackage with only the buildings that are within the AOI. Add another cell that filters all building less than 15 sq meters and rerun the notebook

### 2nd prompt: data from OSM

We are working in a livability score for all buildings in the Maldonado/Punta del Este conglomerate, in Uruguay.
I need you to download some layers from OSM, using osmnx. All data must be within a 10 km buffer from the AOI (data\buildings_aoi.gpkg). Store all layers inside data, and in geopackage folder.
These are the layers I need:
- Green areas: parks, squares, forests and so on.
- Public transportation nodes and hubs: highway=bus_stop, amenity=bus_station
- Roads/street network
- Amenities: amenity=restaurant, cafe, bar
- Coastlines and beaches: natural=beach, natural=coastline, leisure=beach_resort

So, edit the Jupyter Notebook called "02_download_osm_data.ipynb", adding cells for every layer needed.


### 3rd prompt: linear calculations

Now we are ready to make our first calculations.
Make a Jupyter Notebook to calculate all the linear distances from every building in data\buildings_aoi.gpkg to the closest feature in the layers:
data\geopackage\amenities.gpkg
data\geopackage\coast_beaches.gpkg
data\geopackage\green_areas.gpkg
data\geopackage\public_transport.gpkg
data\geopackage\street_network.gpkg

I'll also need the total number of parks within a 500 meters range and also for amenities (buffer analysis).
Export a geopackage with all the buildings plus this calculated data.
Plot maps inside the notebook so I can have a glimpse of what you did.

Do you suggest something extra for this analysis?


### 4th prompt: network distance

I want a more complex analysis. Departing from the notebook "03_proximity_analysis.ipynb", create a new one called "04_network_analysis.ipynb", and replace the linear distance and buffering analysis by network distance and isochrones.
Use OSMnx for this calculations, if possible, reuse the network "data\geopackage\street_network.gpkg". Otherwise, choose an alternative working solution. Ultimately, we can use OpenRouteService API (I'll provide an API key).
These are the metrics I want:
Network distance to the 5 closest amenities
Network distance to the 5 closest green areas
Netwrok distance to the closes transport hub
Network distance to the closest beach
Network distance to the coast
Total number of parks within a 15 minutes walking isocrhone
Total number of amenities within a 15 minutes walking isocrhone

Normalize all the data, and export a geopackage with all the buildings plus this calculated data.
Plot maps inside the notebook so I can have a glimpse of what you did.

Do you suggest something extra for this analysis?


### 5th prompt: index

Add a final cell computing one single index that's based on all the data you calculated:
dist_cols = ["nd_amenity5_m", "nd_green5_m", "nd_hub_m", "nd_bus_stop_m", "nd_beach_m", "nd_coast_m", "detour_amenity"]
pos_cols = ["parks_15min", "amenities_15min", "bus_stops_15min"]

Maybe nd_coast_m & nd_beach_m should be pondered, since if not the index will be practically a proxy of the distance to the beach.

What do you think?


### Results