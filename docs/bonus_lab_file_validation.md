# Azure Data Factory Project: file validation

## Project Overview
Implement validated file transfer pipeline that validates that the csv files in .txt format only have 5 columns before transferring each such file

## Requirements
- parametrize the pipeline for the source folder and the column count
- scan the /landing_customer_orders for txt files
- for each such file only copy the files that have 5 columns using the inbound order items dataset
