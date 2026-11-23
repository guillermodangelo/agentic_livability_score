# Agentic livability score for all buildings in the Maldonado/Punta del Este conglomerate

## Introduction

Maldonado and Punta del Este are two coastal cities placed in the Maldonado department, in the East of Uruguay. Punta del Este is a well know tourist destination, 
so during the summer it receives a big contingent of high income tourists from all
over the world, but mainly from Argentina.

In this project I created a livabilty score, prompting Claude to download
geospatial data and generate some spatial calculations, for which I consider
are some features that make a city "livable" and al culturally aligned with
the taste of the uruguayan population.

The score and the selection of the variable has no other theoretical
base but my own decisions, and is neither is backed by research. It's just my personal
interpretation of what people would expect to enjoy while living in a city, 
restricted by the data availability and completeness.

## Key data

Building footprints come from the [VIDA Google-Microsoft Open Buildings](https://source.coop/vida/google-microsoft-open-buildings) dataset (78,359 buildings).
All other data comes from OpenStreetMap, accessed through osmnx:

| Layer | OSM tags |
|---|---|
| Coastline | `natural=coastline` |
| Beaches | `natural=beach` |
| Green areas | `leisure=park/garden/playground`, `place=square` (parks); plus forests, grass, woods, etc. |
| Amenities | `amenity=restaurant/cafe/bar` |
| Public transport hubs | `amenity=bus_station`, `public_transport=station` |
| Bus stops | `highway=bus_stop` |
| Street network | all street types (`network_type="all"`) |

## The score

All distances are walking distances along the street network, not straight lines. A 15-minute walk is taken as 1,200 m.

The variables measured were:

| Theme | Variable |
|---|---|
| Services | Mean distance to the 5 nearest amenities |
| | Amenities within a 15-minute walk |
| | Detour index: walking distance to the nearest amenity divided by the straight-line distance |
| Transport | Distance to the nearest bus stop |
| | Bus stops within a 15-minute walk |
| | Distance to the nearest transport hub |
| Green | Mean distance to the 5 nearest green areas |
| | Parks within a 15-minute walk |
| Coast | Distance to the nearest beach |
| | Distance to the coastline |

Each variable was capped at its 95th percentile and scaled from 0 to 1, with 1 always meaning better. Variables were averaged within each theme, then the themes were combined with these weights: services 0.35, transport 0.25, green 0.25 and coast 0.15. The result is a single `livability` score from 0 to 100.

The coast gets a low weight on purpose. Otherwise the score would mostly measure distance to the beach, since most amenities also sit near the coast.

