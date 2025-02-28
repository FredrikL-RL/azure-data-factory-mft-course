# Lab 3: Automated Alert and Logging System

## Objective
Create automated failure notifications and setup logging

## Points covered
- Azure Monitor Metrics
- Azure Monitor Alerts
- Copy Activity Logging

## Steps

### 1. Configure Storage Account Permissions
- Access IAM for dlsadfcourselognamedev001
- Assign roles to data factory:
  - Storage Blob Data Contributor
  - Storage Blob Data Reader

### 2. Setup Logging Infrastructure
- Create logs container
- Create linked service to DLS logging storage account

### 3. Create Datasets
- CSV dataset source: 
  - Point to landing_customer_orders folder in SFTP
- JSON dataset sink:
  - Point to inbound/order_items in DLS

### 4. Make new pipeline
- create new pipeline and copy activity inside of it
- use above datasets
- import mapping and set quantity column to be cast to int
- Enable log setting in copy activity
- Specify log container
- Check skip incompatible rows
- Choose either warning or info level

### 5. Test Logging
- Run the pipeline
- Verify logs in the logs container of DLS

### 6. Create Failure Scenario
- Create a new pipeline with a fail activity
- Save and publish

### 7. Setup Alert System
- Create alert with quick action group
- Configure email notification
- Set alert metric to failed pipelines

### 8. Test Alert System
- Trigger the fail pipeline
- Confirm receipt of alert email

## Notes
- Logging levels (warning vs info) will affect the detail of logs generated
- Ensure all permissions are correctly set for seamless operation
- Regularly review and adjust alert configurations as needed

## References
- [Data Factory monitoring](https://learn.microsoft.com/en-us/azure/data-factory/monitor-data-factory)
- [Copy activity logs](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-log?tabs=data-factory)
- [programmatic monitoring with API](https://learn.microsoft.com/en-us/azure/data-factory/monitor-programmatically)
