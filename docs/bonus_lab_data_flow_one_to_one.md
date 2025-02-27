# Azure Data Factory Project: One-to-One Data Flow Processing

## Project Overview
Implement a data standardization pipeline in Azure Data Factory that uses data flow to processes multiple input files and generates an equal number of output files with the same name as inputted

## Requirements
- parametrize the pipeline for the source and dest folders
- send the data from sftp stores/current_date --> dls standardized/stores/currents_date with the same file name in src and dest
- use the previous data flow to standardize
- use the get metadata, filter and for each activity to execute the standardization data flow
