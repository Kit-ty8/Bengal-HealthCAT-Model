# Bengal-HealthCAT-Model
Geospatial catastrophe (CAT) model quantifying healthcare infrastructure risk in WB and Odisha.

Bengal HealthCAT: Coastal Cyclone Exposure & Risk Model

Overview

Bengal HealthCAT is a geospatial catastrophe (CAT) model designed to quantify the physical vulnerability and exposure of healthcare infrastructure in West Bengal and Odisha to severe cyclonic storms.
This project processes a quarter-century of historical cyclone data (1999–2024) to simulate wind hazard footprints and calculate Mean Damage Ratios (MDR) for regional hospitals. The model bridges meteorological hazard data with infrastructural exposure to generate structured risk metrics for 31,500 facility-impact scenarios.

Technical Stack
Languages: Python (Geospatial & Vulnerability Engine)
Libraries: GeoPandas, Pandas, NumPy, Shapely
Coordinate Reference System (CRS): India Metric CRS (EPSG:32645)

Project Architecture & Progress

✅ Phase 1: Data Acquisition & Preprocessing

Hazard Data: Ingested global IBTrACS North Indian Ocean cyclone tracks (GeoJSON).
Exposure Data: Sourced and cleaned Humanitarian Data Exchange (HDX) healthcare facility points for West Bengal and Odisha.
Refinement: Filtered global datasets down to the Bay of Bengal basin, explicitly isolating severe historical events including the 1999 Odisha Super Cyclone, Aila, Fani, Amphan, Yaas, and Dana.

✅ Phase 2: Spatial Engine Setup

Reprojected all geospatial geometries from standard WGS 84 (decimal degrees) to EPSG:32645 (metric meters) to enable precise physical distance calculations.
Standardized meteorological data by addressing historical wind speed gaps using basin-specific classifications (e.g., applying a 34-knot baseline for minimum cyclonic storm thresholds).

✅ Phase 3: Hazard & Vulnerability Modeling

Wind Footprint Generation: Programmed a spatial .buffer() to construct 50km destructive wind swaths around the historical storm tracks.
Exposure Intersection: Executed a spatial join (gpd.sjoin) to identify the exact facilities caught within the destructive radius of each event.
Vulnerability Engine: Developed and applied a logistic S-Curve function ($v_{half} = 100$, $k = 0.05$) to translate local wind speeds into a Mean Damage Ratio (MDR) for every affected facility.
Output: Generated a batch-processed master dataset of 31,500 structural damage records ready for database ingestion.

⏳ Phase 4: Database Architecture & Financial Loss (In Progress)

Transitioning processed exposure data into a structured SQL Star Schema.
Joining physical damage ratios (MDR) with facility replacement values to calculate modeled financial losses and spatial risk aggregations.

