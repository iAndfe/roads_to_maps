# Roads to Maps

This Jupyter Notebook is an implementation of road safety corridors analysis using pandas, geopandas, shapely, and fuzzywuzzy. The goal of this implementation is to join corridor information with LINZ road data, process the merged data, and create meaningful geospatial files for visualization and further analysis.


## Dependencies

Ensure that you have the following Python libraries installed to use this Jupyter Notebook:

- pandas
- fuzzywuzzy
- geopandas
- shapely

You can install them using the following command:

```bash
pip install -r requirements.txt
```

## Input Data

The notebook expects the following input files in the `input` folder:

- `sw.csv`: The CSV file containing the corridor information.

The notebook also expects LINZ roads files in the `linz_roads` folder:

- `nz-roads-addressing.csv`: The CSV file containing LINZ road data.
- `roads.shp`: The shapefile for LINZ road data.

## Output Data

The notebook produces the following output files in the `joined` folder:

- `join_table.csv`: The CSV file containing the joined LINZ roads and corridors data.
- `not_joined.csv`: The CSV file with corridor rows that didn't match any LINZ roads.
- `with_gps.csv`: The CSV file with rows that have GPS coordinates.
- `without_gps.csv`: The CSV file with rows that do not have GPS coordinates.

The notebook also creates a final output file, `output/output.shp`, which is the combination of both GPS and non-GPS data as a shapefile for further geospatial analysis.


## How to Run

1. Ensure you have installed the dependencies mentioned above.
2. Place your input data files in the appropriate directories as mentioned in the "Input Data" section.
3. Run the Jupyter Notebook cells in order.
4. Check the output files in the `joined` folder and the final output in the `output` folder.


## Notebook Overview

The notebook consists of the following sections and descriptions:

1. Importing libraries
2. Helper functions for preprocessing, fuzzy matching, and manipulating geospatial data.
3. Function to join corridors and LINZ data based on road names.
4. Preprocess the joined data, split it into with and without GPS coordinates.
5. Process the data without GPS to create a GeoDataFrame.
6. Combine the GeoDataFrames of the with-GPS and without-GPS data.
7. Save the combined GeoDataFrame to a shapefile in the output folder.

Please refer to the inline comments and markdown cells in the Jupyter Notebook for a detailed understanding of each step.

## How to Use

1. Ensure that you have the proper Python environment set up and dependencies installed as mentioned above.
2. Place your input files (corridor CSV file and LINZ roads files) in the appropriate folders as mentioned in the "Input Data" section.
3. Open the Jupyter Notebook and run the notebook cells in sequential order from top to bottom. Wait for each cell to execute completely before moving on to the next one.
4. Monitor the progress of the data processing as the code runs. The final output will be saved in the `output` folder, and intermediate outputs will be saved in the `joined` folder.

## Caveats and Tips

- The quality of the results is dependent on the quality of the initial data. Make sure your data is clean, formatted correctly, and consistent to ensure the best results.
- When performing the fuzzy matching, you might need to adjust the `threshold` value based on your specific use case. A higher threshold will result in stricter matching and potentially fewer matches, while a lower threshold will result in more lenient matching with potentially more false positives.
- Be mindful of the coordinate reference systems (CRS) of your shapefiles. Ensure that your data is in the correct CRS for accurate geospatial analysis. If your data comes in a different CRS, you can use the `to_crs()` function in GeoPandas to convert it to the right one.
- The script currently drops rows where the 'geometry_road' is a `MultiLineString`. If your dataset contains a significant number of `MultiLineString` geometries, this may result in a large amount of data being excluded. You may need to adjust this part of the script to better handle `MultiLineString` geometries depending on your dataset and use case.

## Troubleshooting

1. **Issues installing the required libraries**: Make sure you're running a version of Python that's compatible with all the libraries (Python 3 is recommended). If you're using pip to install, try upgrading pip with `pip install --upgrade pip`. 

2. **Errors when running the script**: Check the error message for hints about what's going wrong. If the error is related to a specific line of code, check that part of the script to see if there are any obvious issues.

3. **Output doesn't look right or missing expected matches**: Check the `threshold` value in the fuzzy matching step. If it's set too high, you may be missing valid matches. Conversely, if it's set too low, you may be getting incorrect matches.

For further assistance, you can refer to the documentation of the libraries used: [Pandas](https://pandas.pydata.org/docs/), [FuzzyWuzzy](https://github.com/seatgeek/fuzzywuzzy), [GeoPandas](https://geopandas.org/), [Shapely](https://shapely.readthedocs.io/en/stable/), and [NumPy](https://numpy.org/doc/). You can also ask for help on forums like Stack Overflow, making sure to provide all necessary details to understand your problem.