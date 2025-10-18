# House Orientation Analysis

## Overview

This project analyzes property orientations by determining which direction each house faces (North, South, East, West, etc.) using spatial analysis of cadastral data, road networks, and address information.

## Objective

Find out for every house which direction it faces and produce an output file with one row per property containing address and orientation columns.

## Features

- **Spatial Analysis**: Links addresses to parcels and roads using geospatial joins
- **Orientation Calculation**: Determines house frontage by finding parcel edges closest to roads
- **Robust Handling**: Supports both single polygons and multipolygons
- **Clean Output**: Generates CSV file with address and compass direction for each property

## Requirements

- Python 3.7+
- GeoPandas
- Shapely
- Pandas
- NumPy

## Installation

```bash
pip install geopandas shapely pyproj rtree fiona pandas numpy
```

## Data Structure

The project expects the following data files in a `dataset/` folder:

- `cadastre.gpkg` - Property boundary polygons
- `roads.gpkg` - Road centerline data
- `gnaf_prop.parquet` - Address data with coordinates

## Usage

1. Place your data files in the `dataset/` directory
2. Run the Jupyter notebook `code.ipynb`
3. The analysis will generate `house_orientations.csv` with results

## Output

The final CSV file contains:

- **address**: Property address
- **orientation**: Compass direction (N, NE, E, SE, S, SW, W, NW)

## Methodology

1. **Data Loading**: Load cadastral, road, and address datasets
2. **Spatial Joins**: Link addresses to nearest parcels and roads
3. **Edge Analysis**: Find parcel edges closest to roads (frontage)
4. **Bearing Calculation**: Calculate compass direction from house to frontage
5. **Output Generation**: Create CSV with address and orientation data

## Example Results

```
address,orientation
123 Main St,N
456 Oak Ave,NE
789 Pine Rd,S
```

## Technical Details

- Uses UTM coordinate system for accurate distance calculations
- Handles complex geometries including MultiPolygons
- Includes error handling for missing or invalid data
- Tests on small samples before processing full datasets

## License

MIT License

## Contributing

Feel free to submit issues and enhancement requests!
