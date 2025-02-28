# Lab 2: Data Standardization Pipeline

## Objective
Build a Parametrized Data Standardization Pipeline.

### Requirements
- data transferred as below with one data flow
    - SFTP stores/{todays_date}/Online to DLS .../standardize/onlines
    - SFTP outbound/landing_customer_orders/stores to DLS standardized/customer/
- transformations
   - Remove store_id
   - Map coordinates to doubles
   - Add UPDATED_TIMESTAMP using current time

## Points Covered
- Light Transformations
- Debug Pipelines
- Data preview usage

## Steps

### 1. Create Datasets
- Create dataset for inbound DLS (stores/standardized/param)
- Create dataset for outbound SFTP
- Add parameters for both and add them into the dynamic content for folder path

### 2. Create Data Flow
- Set SFTP dataset as source
- Add transformations:
  - Select: Remove store_id
  - Cast: Map coordinates to doubles
  - Derived Column: Add UPDATED_TIMESTAMP
- Create sink to standardized folder

### 3. Create Pipeline
- Add two data flow activities
- Configure parameters:
  - SFTP stores/todays_date/Online to .../standardize/online in DLS
  - SFTP outbound/landing_customer_orders/stores to standardized/customer/
- Run pipeline

## Bonus Tasks

### Homepage Default
- substitute web_address nulls with default 'www.homepage.com'
- Append '/storename' (stripped/substituted spaces)

### Dynamic File Processing
- Use Get Metadata activity
- Implement ForEach operator
- Parametrize data flow for one-to-one file processing

## Debugging

- Use debug mode for intermediate results
- Set breakpoints on faulty activities
- Chain activities for targeted debugging

## References
- [Data Flows Overview](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-overview)
- [Data Flow Partitioning and Performance](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-performance)
- [Parameters and Variables](https://learn.microsoft.com/en-us/azure/data-factory/concepts-parameters-variables)
- [Iterative development and debugging](https://learn.microsoft.com/en-us/azure/data-factory/iterative-development-debugging?tabs=data-factory)
- [Data flow debug mode](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-debug-mode?tabs=data-factory)
- [Copy activity monitoring](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-monitoring?tabs=data-factory)
