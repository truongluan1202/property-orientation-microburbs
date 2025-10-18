# House Orientation Analysis

## Overview

This project analyzes property orientations by determining which direction each house faces (North, South, East, West, etc.) using spatial analysis of cadastral data, road networks, and address information.

## Objective

Find out for every house which direction it faces and produce an output file with one row per property containing property ID, address, and orientation columns.

## Features

- **Spatial Analysis**: Links addresses to parcels and roads using geospatial joins
- **Orientation Calculation**: Determines house frontage by finding parcel edges closest to roads
- **Robust Handling**: Supports both single polygons and multipolygons
- **Clean Output**: Generates CSV file with property ID, address, and compass direction for each property

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
3. The analysis will generate `house_orientations_improved.csv` with results

## Output

The final CSV file contains:

- **property_id**: Property identifier (e.g., NSW3617729)
- **address**: Full street address (e.g., 123 Main Street, Suburb, State 2000)
- **orientation**: Compass direction (N, NE, E, SE, S, SW, W, NW)

## Methodology

1. **Data Loading**: Load cadastral, road, and address datasets
2. **Spatial Joins**: Link addresses to nearest parcels and roads
3. **Edge Analysis**: Find parcel edges closest to roads (frontage)
4. **Bearing Calculation**: Calculate compass direction from house to frontage
5. **Address Enhancement**: Map property IDs to proper street addresses
6. **Output Generation**: Create CSV with property ID, address, and orientation data
7. **Data Quality Analysis**: Analyze results to validate analysis quality and show insights

## Example Results

```
property_id,address,orientation
NSW3617729,123 Main Street, Suburb, State 2000,N
NSW3617730,456 Oak Avenue, Suburb, State 2000,NE
NSW3617731,789 Pine Road, Suburb, State 2000,S
```

## Data Quality Insights

- **617,622 properties** analyzed from **361 unique addresses**
- **High-density urban data**: ~1,700 properties per address (apartment complexes)
- **Realistic complexity**: Same address, different orientations (units face different directions)
- **Comprehensive coverage**: Every property analyzed individually
- **Orientation distribution**: E (30.9%), SE (24.0%), N (16.2%), NW (15.5%), etc.

## Technical Details

- Uses UTM coordinate system for accurate distance calculations
- Handles complex geometries including MultiPolygons
- Includes error handling for missing or invalid data
- Tests on small samples before processing full datasets

## License

MIT License

## Contributing

Feel free to submit issues and enhancement requests!
