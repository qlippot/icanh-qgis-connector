# icanh-qgis-connector
A Python script to connect the ICANH Geovisor API to QGIS and flatten relational archaeological data.
# ICANH Geovisor to QGIS Connector

**Author:** Fernando Suescún
**Status:** Complete

## The Problem
The Colombian Institute of Anthropology and History (ICANH) exposes critical archaeological data via an ArcGIS REST FeatureServer. However, the data is highly normalized across 5 separate layers (Sites, Contexts, Dates, Sources, Collections). 

Standard GIS clients (like QGIS) fail to automatically resolve these 1-to-Many relationships. Researchers are forced to manually download and join multiple tables, which is time-consuming and prone to error. Additionally, the API enforces a 2000-record limit, meaning standard queries miss the vast majority of the ~20,000 archaeological sites.

## The Solution
I developed a Python script for QGIS that acts as a live data bridge. It automatically:
1. **Paginates through the API** to fetch all 20,000+ spatial points and their related tables.
2. **Bypasses the slow SQL engine** by using Python hash-maps (`defaultdict`) to aggregate the relational data in memory.
3. **Handles mixed relational keys** (matching Integer IDs to UUIDs dynamically).
4. **Generates a flattened, spatial memory layer** in QGIS, concatenating all related dates, authors, library codes, and findings into a single, exportable row per site.

## How to Use
1. Open QGIS and open the Python Console.
2. Open the Python Editor (the notepad icon).
3. Copy the contents of `icanh_loader.py` into the editor.
4. Click "Run Script".
5. The script will generate a new layer called `Sitios_ICANH`. Open the Attribute Table to view the flattened data, and export to CSV/Excel.

## Tech Stack
*   Python
*   QGIS PyQGIS API (`qgis.core`)
*   ArcGIS REST API
