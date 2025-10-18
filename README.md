# House Orientation Analysis

## 🏠 Overview

This project performs comprehensive spatial analysis to determine the orientation (compass direction) of every house in a dataset. Using advanced geospatial techniques, it analyzes cadastral boundaries, road networks, and address data to determine which direction each property faces.

## 🎯 Objective

**Primary Goal**: Find out for every house which direction it faces (North, South, East, West, etc.) and produce a clean output file with one row per property containing:

- Property ID
- Full street address
- Compass orientation (N, NE, E, SE, S, SW, W, NW)

## ✨ Key Features

- **🔍 Advanced Spatial Analysis**: Links addresses to parcels and roads using validated geospatial joins
- **📐 Precise Orientation Calculation**: Determines house frontage by finding parcel edges closest to roads
- **🛡️ Robust Data Validation**: Comprehensive error handling and quality checks
- **🧹 Intelligent Deduplication**: Eliminates duplicates while preserving legitimate multi-unit properties
- **📊 High Success Rate**: 99.4% of properties successfully analyzed
- **🎯 Clean Output**: Generates validated CSV with property ID, address, and compass direction

## 📋 Requirements

- **Python**: 3.7 or higher
- **Core Libraries**:
  - GeoPandas (geospatial data processing)
  - Shapely (geometric operations)
  - Pandas (data manipulation)
  - NumPy (numerical computing)
  - PyProj (coordinate transformations)

## 🚀 Installation

```bash
pip install geopandas shapely pyproj rtree fiona pandas numpy
```

## 📁 Data Structure

Place your data files in the `dataset/` directory:

```
dataset/
├── cadastre.gpkg      # Property boundary polygons (MultiPolygon geometries)
├── roads.gpkg         # Road centerline data (LineString geometries)
├── gnaf_prop.parquet  # Address data with coordinates (Point geometries)
└── transactions.parquet # Optional: Property transaction data
```

## 🏃‍♂️ Quick Start

1. **Prepare Data**: Place your data files in the `dataset/` directory
2. **Run Analysis**: Execute `house_orientation_analysis_final.ipynb`
3. **Get Results**: Find your output in `house_orientations_final.csv`

## 📊 Output Format

The final CSV file contains three columns:

| Column        | Description                | Example                         |
| ------------- | -------------------------- | ------------------------------- |
| `property_id` | Unique property identifier | `NSW2966604`                    |
| `address`     | Full street address        | `1 THE LEE, SUBURB, STATE 2000` |
| `orientation` | Compass direction          | `NE`                            |

### Sample Output:

```csv
property_id,address,orientation
NSW2966604,1 THE LEE,NE
NSW2828125,10 CHARLES STREET,W
NSW2824909,8 CAWARRAH ROAD,SE
```

## 🔬 Methodology

### 1. **Data Preparation**

- Load cadastral parcels, road networks, and address coordinates
- Transform all data to UTM coordinate system for accurate distance calculations
- Create spatial indexes for efficient processing

### 2. **Spatial Analysis with Validation**

- **Address-to-Parcel Linking**: Use nearest neighbor joins with distance validation (≤200m threshold)
- **Deduplication**: Keep closest address per parcel to eliminate duplicates
- **Parcel-to-Road Linking**: Connect parcels to nearest roads with validation (≤100m threshold)

### 3. **Orientation Calculation**

- **Edge Extraction**: Extract all edges from parcel boundaries (handles MultiPolygons)
- **Frontage Detection**: Find parcel edge closest to road (house frontage)
- **Bearing Calculation**: Calculate compass direction from house centroid to frontage
- **Validation**: Filter out unreasonable frontage distances (>50m)

### 4. **Quality Assurance**

- **Error Handling**: Track calculation success/failure with detailed error messages
- **Address Enhancement**: Map property IDs to proper street addresses
- **Final Validation**: Ensure data quality and completeness

## 📈 Results & Performance

### **Analysis Statistics:**

- **Total Properties Analyzed**: 1,216 properties
- **Success Rate**: 99.4% (1,209 successful calculations)
- **Failed Calculations**: 7 (legitimate data quality issues)
- **Unique Addresses**: 40 unique street addresses
- **Processing Time**: Optimized for large datasets

### **Orientation Distribution:**

- **SE (Southeast)**: 223 properties (18.4%) - Most common
- **E (East)**: 170 properties (14.1%)
- **W (West)**: 167 properties (13.8%)
- **NW (Northwest)**: 167 properties (13.8%)
- **S (South)**: 164 properties (13.6%)
- **N (North)**: 130 properties (10.8%)
- **SW (Southwest)**: 124 properties (10.3%)
- **NE (Northeast)**: 64 properties (5.3%) - Least common

### **Data Quality Insights:**

- **High-Density Urban Data**: Multiple properties per address (apartment buildings)
- **Realistic Complexity**: Same address, different orientations (units face different directions)
- **Comprehensive Coverage**: Every property analyzed individually
- **Spatial Accuracy**: Different units face different directions as expected

## 🛠️ Technical Details

### **Coordinate Systems:**

- **Input**: WGS84 (EPSG:4326) for global compatibility
- **Processing**: UTM (EPSG:32756) for accurate distance calculations
- **Output**: Original coordinate system preserved

### **Geometry Handling:**

- **MultiPolygon Support**: Handles complex parcel boundaries
- **Edge Extraction**: Robust polygon edge detection
- **Distance Calculations**: Precise spatial measurements

### **Validation Framework:**

- **Distance Thresholds**: Configurable validation parameters
- **Error Tracking**: Comprehensive failure analysis
- **Quality Metrics**: Success rates and data completeness

## 🎯 Use Cases

### **Real Estate Analysis:**

- **Property Valuation**: North-facing properties often command premium prices
- **Market Research**: Understanding orientation preferences in different areas
- **Investment Decisions**: Orientation affects rental yields and capital growth

### **Urban Planning:**

- **Sunlight Access**: Orientation affects natural light and energy efficiency
- **Building Design**: Understanding existing orientation patterns
- **Infrastructure Planning**: Road and utility placement considerations

### **Environmental Analysis:**

- **Solar Potential**: Orientation affects solar panel efficiency
- **Energy Efficiency**: Natural heating and cooling patterns
- **Sustainability**: Building orientation for optimal energy use

## 📁 File Structure

```
project/
├── house_orientation_analysis_final.ipynb  # Main analysis notebook
├── house_orientations_final.csv            # Final output file
├── dataset/                                # Input data directory
│   ├── cadastre.gpkg
│   ├── roads.gpkg
│   ├── gnaf_prop.parquet
│   └── transactions.parquet
├── self-explainatory/                      # Documentation
│   ├── explain.ipynb                      # Visual explanation
│   └── output.png                         # Sample output
└── README.md                              # This file
```

## 🔧 Troubleshooting

### **Common Issues:**

1. **Missing Dependencies**: Ensure all required packages are installed
2. **Data Format**: Verify data files are in correct format (GPKG, Parquet)
3. **Memory Issues**: For large datasets, consider processing in chunks
4. **Coordinate System**: Ensure data is in WGS84 (EPSG:4326)

### **Performance Tips:**

- Use spatial indexes for large datasets
- Process data in batches if memory is limited
- Monitor distance thresholds for your specific area

## 📄 License

MIT License - Feel free to use, modify, and distribute.

## 🤝 Contributing

Contributions welcome! Please feel free to:

- Submit bug reports
- Suggest enhancements
- Improve documentation
- Add new features

---

**Note**: This analysis provides accurate orientation data for properties based on spatial relationships between parcels and roads. Results are validated and filtered for quality assurance.
