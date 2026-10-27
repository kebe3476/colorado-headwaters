# Headwaters: Colorado Snow to Rivers

An animated map of Colorado's water supply: snow building and melting across the mountains, rivers rising as the melt arrives, and reservoirs filling downstream, for every water year since October 2004. It runs on an Airflow, Databricks (Delta Lake), and dbt pipeline that backfills full history and then updates daily. Work in progress; see Status.

<!-- The only public doc in this repo. Never name or link internal files. Keep in sync with the design doc. -->

## How it works (planned design)

Snow comes from SNODAS, a daily national snow model on a roughly 1 km grid. Each day's file is downloaded, clipped to Colorado, and stored two ways: as H3 hexagon cells for analysis, where snow joins cleanly to basins and stations, and as the original grid for the map, so the snow layer keeps its full detail. River flow and reservoir storage come from public federal and state APIs. dbt models everything into daily facts and marts, and an export step writes small per-day files that the map plays back.

## Stack

| Layer | Tool |
|---|---|
| Orchestration | Airflow |
| Storage and compute | Databricks, Delta Lake |
| Spatial indexing | H3 |
| Transformation and modeling | dbt (dbt-databricks) |
| Map | MapLibre GL JS, deck.gl (kepler.gl for the first prototype) |

## Sources

| Source | What it provides |
|---|---|
| NOAA SNODAS | Daily modeled snow water equivalent, depth, and melt, ~1 km grid, October 2004 onward |
| NRCS SNOTEL | Measured snow at mountain stations, used to validate SNODAS |
| USGS Water Data APIs | Daily river flow at stream gauges |
| Bureau of Reclamation RISE | Reservoir storage, elevation, and releases |
| Colorado CDSS (planned) | State reservoirs and transmountain diversion tunnel flows |
| USGS WBD, hydrography, 3DEP | Basin boundaries, river network, elevation |

## Status

Planning and source verification. The design and data contract are written and a prototype on simulated data exists; pipeline work has not started.

## Setup

Not yet. Exact commands will be added once there is something to set up.
