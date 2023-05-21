# Processing and Analyzing Road Networks

This script is used to process and analyze road networks data. It reads data from .csv files, performs fuzzy matching on road names, merges dataframes, and then applies several geospatial processing tasks using GeoPandas and Shapely.

## Script Description

1. The script starts by importing required libraries: `pandas`, `fuzzywuzzy`, `geopandas`, `shapely`, `ast`, and `numpy`.

2. It defines helper functions for preprocessing road names, fuzzy matching road names, converting coordinates to `Point` objects, and checking if a geometry object is a `LineString`.

3. The `process_csv` function is defined. This function reads two .csv files and performs fuzzy matching on road names. The function returns a dataframe containing matched roads.

4. The script then calls `process_csv` function with a .csv file. It then filters columns and removes duplicates and rows with missing GPS coordinates. The processed dataframe is saved to a .csv file.

5. A GeoDataFrame is read from a .shp file (shapefile). The dataframe read from the .csv file is then converted to a GeoDataFrame, with 'StartPoint' as the geometry column.

6. The script then merges the two GeoDataFrames based on 'road_id'. It applies the `is_linestring` function to filter out rows where 'geometry_road' is a MultiLineString.

7. The script defines a function for finding the closest point on a line to a given point. This function is applied to find the closest points on the roads to the start and end points.

8. A function is defined to cut a `LineString` at two points. This function is then applied to cut the road lines at the start and end points.

9. Unneeded columns are dropped and the 'Road_Segment' column is set as the geometry column.

10. Finally, the processed GeoDataFrame is saved to a shapefile.

## How to Use

1. Prepare your input files: a .csv file for the `process_csv` function and a .shp file for the GeoDataFrame.

2. Run the script in a Jupyter notebook. You can install Jupyter via pip (`pip install jupyter`) or with Anaconda.

3. The script will output a .csv file ('combined.csv') and a shapefile ('output/output.shp'). The .csv file contains data about the roads and the shapefile contains the geometries of the road segments.

## Requirements

This script requires Python 3 and the following libraries: `pandas`, `fuzzywuzzy`, `geopandas`, `shapely`, `ast`, and `numpy`. You can install these libraries via pip:

```
pip install pandas fuzzywuzzy geopandas shapely numpy
```

Note: the `fuzzywuzzy` library also requires the `python-Levenshtein` library to speed up processing. You can install it via pip:

```
pip install python-Levenshtein
```

## Caveats and Tips

1. Make sure your input CSV and shapefile follow the correct format that the script expects. Misformatted files can cause errors in execution.

2. Be mindful of the coordinate system of your shapefiles. It's crucial to ensure your data is in the correct spatial reference for accurate geospatial analysis. If your data comes in a different coordinate system, you can use the `to_crs()` function in GeoPandas to convert it to the right one.

3. When performing the fuzzy matching, you might need to adjust the `threshold` value based on your specific use case. A higher threshold will result in stricter matching, potentially leading to fewer matches.

4. The script uses the `Start GPS Co-ordinates` and `End GPS Co-ordinates` columns to determine the start and end points of each road segment. If your dataset uses different column names, you'll need to adjust the script accordingly.

5. The script currently drops rows where the 'geometry_road' is a `MultiLineString`. If your dataset contains a significant number of `MultiLineString` geometries, this may result in a large amount of data being excluded. You may need to adjust this part of the script to better handle `MultiLineString` geometries, depending on your dataset and use case.

6. Keep in mind that the quality of your fuzzy match and subsequent analysis is highly dependent on the quality of your data. Ensure your data is clean and consistent for the best results.

## Troubleshooting

1. **If you're experiencing issues installing the required libraries**: Make sure you're running a version of Python that's compatible with all the libraries (Python 3 is recommended). If you're using pip to install, try upgrading pip with `pip install --upgrade pip`. 

2. **If you're encountering errors when running the script**: Check the error message for hints about what's going wrong. If the error is related to a specific line of code, check that part of the script to see if there are any obvious issues.

3. **If the output doesn't look right or you're missing expected matches**: Check the `threshold` value in the fuzzy matching step. If it's set too high, you may be missing valid matches. Conversely, if it's set too low, you may be getting incorrect matches.

For further assistance, you can refer to the documentation of the libraries used: [Pandas](https://pandas.pydata.org/docs/), [FuzzyWuzzy](https://github.com/seatgeek/fuzzywuzzy), [GeoPandas](https://geopandas.org/), [Shapely](https://shapely.readthedocs.io/en/stable/), [ast](https://docs.python.org/3/library/ast.html) and [NumPy](https://numpy.org/doc/). You can also ask for help on forums like Stack Overflow, making sure to provide all necessary details to understand your problem.
