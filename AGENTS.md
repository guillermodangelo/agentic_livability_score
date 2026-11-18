# Agentic livability score for all buildings in the Maldonado/Punta del Este conglomerate

## 1. General instructions and restrictions

- Do not access any directory in my file system other than this and all directories contained in this one.
- If you need to save something temporally, create a temp folder in this directory and delete it after
- Use Python for all coding tasks
- Use the uv virtual environment called .venv
- If a library is needed nad is not present, install it in the virtual environment
- All downloaded data must be stored in the "data" folder
- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.
- Touch only what you must. Clean up only your own mess.

## 2. Coding and geoprocessing

- Imports go at the beginning of the notebook
- For vector geoprocessing prefer Geopandas
- Work in Jupyter Notebooks, but save outputs if asked for
- For base maps, both static of interactive maps, prefer OSM over other sources that may require an API key.


## 3. How to obtain the data

- If specific sources are pointed in the prompt, prefer those sources over the following recommendations

- For the building footprints, use the VIDA footprints for Uruguay (URY): 
https://source.coop/vida/google-microsoft-open-buildings/geoparquet/by_country/country_iso=URY

- For all other data, you may download OSM data using osmnx library


## 4. Results

- Save the results in the output folder

- The final result is expected to be a geopackage containing all the buildings
within the AOI along with its livability score in a field.