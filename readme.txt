# Road Name Matching

This Python notebook takes a list of road names from different sources and attempts to match them with the official road names provided in the `nz-roads-addressing.csv` file. The script uses fuzzy string matching to find the best match for each road name and outputs the matched road names along with their corresponding road ID and road type (filter, local, or op) in a combined CSV file. Additionally, it outputs the unique and unmatched road names into separate text files.

## Prerequisites

This script requires the following Python libraries:

- pandas
- fuzzywuzzy

You can install them using pip:

```
pip install pandas fuzzywuzzy
```

## Input Files

The notebook takes the following input files:

- `nz-roads-addressing.csv`: A CSV file containing the official road names with their road IDs.
- `shu_raw/filter.csv`: A CSV file containing a list of road names categorized as "filter".
- `shu_raw/local.csv`: A CSV file containing a list of road names categorized as "local".
- `shu_raw/op.csv`: A CSV file containing a list of road names categorized as "op".

## Output Files

The notebook generates the following output files:

- `combined_road_ids.csv`: A CSV file containing the matched road names along with their road ID and road type (filter, local, or op).
- `unique.txt`: A text file containing the unique matched road names sorted alphabetically.
- `unmatched.txt`: A text file containing the unmatched road names sorted alphabetically.

## Workflow

1. Preprocess the road names by extracting the first word and converting it to lowercase.
2. Perform fuzzy string matching to find the best match for each road name in the input files (filter, local, and op) with the official road names in the `nz-roads-addressing.csv` file.
3. Set a threshold for the fuzzy matching score to consider a match as valid.
4. Combine the matched road names and their road types (filter, local, or op) into a single DataFrame.
5. Merge the combined DataFrame with the `nz-roads-addressing.csv` file to obtain the road ID for each matched road name.
6. Save the combined DataFrame with road IDs and road types into the `combined_road_ids.csv` file.
7. Create a list of unique matched road names and save it in the `unique.txt` file.
8. Create a list of unmatched road names and save it in the `unmatched.txt` file.

## How to Run

Use the juptyr notebook file, and press run

After the cell finishes running, you can find the generated output files (`combined_road_ids.csv`, `unique.txt`, and `unmatched.txt`) in the same directory.