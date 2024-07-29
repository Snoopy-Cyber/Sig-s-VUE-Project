# Sig-s-VUE-Project
Extract Data from VUE/ .vrl files

# VUE FILES
To extract specific columns from .vrl files used in VUE (a 3D environment software), you can use PowerShell to parse and extract data. 
However, since .vrl files are typically custom-formatted files used by VUE and may not have a standard structure, you will need to adapt the script based on the specific format of your .vrl files.

For this example, let’s assume .vrl files are text-based and contain data separated by a delimiter (such as a comma or space) and that you want to extract two specific columns. Here’s a PowerShell script to help with this task:

## PowerShell Script to Extract Columns from .vrl Files
* Identify the delimiter used in your .vrl files (e.g., comma, space, tab).
* Determine the column indices you want to extract.


## Here’s a sample script that extracts data from two columns of a .vrl file. This example assumes a comma delimiter, but you can adjust the delimiter as needed.

```shell
# Define the path to the .vrl file
$vrlFilePath = "C:\path\to\yourfile.vrl"  # Update with the actual path

# Define the output file path
$outputFilePath = "C:\path\to\output.csv"  # Update with the desired output path

# Define the delimiter (adjust if needed, e.g., "," for comma, " " for space, "`t" for tab)
$delimiter = ","

# Define the column indices you want to extract (0-based index)
$column1Index = 0
$column2Index = 1

# Read the .vrl file
$content = Get-Content -Path $vrlFilePath

# Process each line
$results = $content | ForEach-Object {
    $columns = $_ -split [regex]::Escape($delimiter)
    if ($columns.Length -gt [Math]::Max($column1Index, $column2Index)) {
        # Extract the desired columns
        $columns[$column1Index] + $delimiter + $columns[$column2Index]
    }
}

# Write the results to the output file
$results | Set-Content -Path $outputFilePath

Write-Output "Data extraction complete. Check the output file at $outputFilePath."

```


## Explanation:
1) Path Definitions:

    * Update $vrlFilePath with the path to your .vrl file.
    * Update $outputFilePath with the path where you want to save the extracted data.

2) Delimiter:

    * Set $delimiter to the appropriate character for your file (e.g., comma for CSV, space, tab).

3) Column Indices:

    * $column1Index and $column2Index specify which columns to extract. Adjust these indices according to the columns you need.

4) Processing:

    * Get-Content reads the file line by line.
    * Each line is split into columns based on the delimiter.
    * The script checks if the line contains enough columns before attempting to extract them.
    * Results are saved to the output file in a CSV format.

## Customization
If your .vrl file format is different or more complex, you may need to adjust the script to handle that format. For example, if the columns are fixed-width or use a different delimiter, modify the splitting logic accordingly.



-----------------------------------------------------------------------------------PYTHON-------------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------VERSION-----------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# PYTHON EDITION

### To extract columns from .vrl files using Python, you can utilize the pandas library for easier manipulation of tabular data or handle the parsing manually if your data format is simple.

### Here’s a Python script that assumes .vrl files are text-based and the columns are separated by a delimiter (e.g., comma, space). The script will read the .vrl file, extract two specific columns, and save the result to a CSV file.

```shell

import pandas as pd

def extract_columns(input_file_path, output_file_path, col1_index, col2_index, delimiter=','):
    """
    Extracts two columns from a .vrl file and saves them to a CSV file.
    
    :param input_file_path: Path to the input .vrl file
    :param output_file_path: Path to the output CSV file
    :param col1_index: Index of the first column to extract (0-based)
    :param col2_index: Index of the second column to extract (0-based)
    :param delimiter: Delimiter used in the .vrl file (default is comma)
    """
    try:
        # Read the .vrl file into a DataFrame
        df = pd.read_csv(input_file_path, delimiter=delimiter, header=None)
        
        # Extract the specified columns
        if col1_index < df.shape[1] and col2_index < df.shape[1]:
            extracted_df = df[[col1_index, col2_index]]
        else:
            raise IndexError("Column index out of range")

        # Save the extracted columns to a CSV file
        extracted_df.to_csv(output_file_path, index=False, header=False)
        
        print(f"Data extraction complete. Check the output file at {output_file_path}")
    
    except FileNotFoundError:
        print(f"Error: The file {input_file_path} was not found.")
    except pd.errors.EmptyDataError:
        print("Error: The file is empty.")
    except IndexError as e:
        print(f"Error: {str(e)}")
    except Exception as e:
        print(f"An unexpected error occurred: {str(e)}")

# Example usage
input_vrl_file = 'path/to/yourfile.vrl'  # Update with your .vrl file path
output_csv_file = 'path/to/output.csv'   # Update with the desired output CSV file path
column1_index = 0  # Update with the index of the first column to extract (0-based)
column2_index = 1  # Update with the index of the second column to extract (0-based)
delimiter = ','    # Update if using a different delimiter

extract_columns(input_vrl_file, output_csv_file, column1_index, column2_index, delimiter)

```

## Explanation:
1) Imports:

    * "pandas" is used to handle data manipulation. Install it via pip install pandas if you don't have it.
2) Function Definition:

    * extract_columns function reads the .vrl file into a pandas DataFrame, extracts the specified columns, and writes them to a CSV file.
3) Error Handling:

    * The script includes basic error handling for file not found, empty file, index out of range, and other unexpected errors.
4) Usage:

    * Update input_vrl_file with the path to your .vrl file.
    * Update output_csv_file with the path where you want to save the extracted columns.
    * Set column1_index and column2_index to the indices of the columns you want to extract (0-based index).
    * Set delimiter according to the delimiter used in your .vrl file (comma is used in the example).
  

## Running the Script

1) Save the script to a '.py' file, e.g., 'extract_column.py'
2) Run the script using Python:
3) ```shell
   python extract_columns.py
   ```
4) This script shold be adaptable to different delimeters and file structures. If your '.vrl' file has a different format, you may need to adjust the 'delimeter' or parsing logic accordingly. 





