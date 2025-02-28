# Lab 1: Scheduled Secure MFT Pipeline

## Objective
Build triggered secure data lake storage → SFTP pipelines with error handling

## Requirements
- Grant ADFs access to dls via system-assigned managed identity
- Give minimized privileges and secure access on sftp via azure key vault and system-assigned managed identity
- data transferred between
    - Source dls outbound stores/todays_date to sink sftp inbound stores/todays_date
- trigger schedule created for once a day

## Points Covered
- Key Vault integration
- Creating secure linked services
- The Copy activity 
- Scheduling
- Dynamic Content

## Steps

### 1. Configure IAM Permissions
- Go into IAM for dlsadfcoursenamedev001
- Give storage blob data contributor and storage blob data reader roles to data factory

### 2. SFTP User Setup
- Go into sftp storage account
- Create a user with SSH password
- Give necessary permissions to the containers (need delete on inbound)
- Copy the password

### 3. Azure Key Vault Configuration
- Give yourself key vault admin
- Give adf key vault reader
- Create a secret and use the password
- Go into the IAM for the key and give Key Vault Secrets User on it

### 4. Create Linked Services
- Azure key vault
- 2 SFTP (inbound and outbound) using azure key vault
- Storage account dlsadfcoursenamedev001

### 5. Create Datasets
- Source dls outbound stores
- Sink sftp inbound stores

### 6. Configure Copy Activity
- Create the copy activity between source and sink datasets
- Use dynamic content to transfer today's dataset into a created today date folder

## Security Enhancements

### Host Key Validation
[SSH fingerprint validation](https://learn.microsoft.com/en-us/azure/storage/blobs/secure-file-transfer-protocol-host-keys)

### Use Public and Secret Key
Use public and secret key not password.

### Enable Secure Transfer
Enable secure transfer on storage accounts

### Disable Access Keys
Disable access keys authorization on resources, if you have disabled access keys you need to give yourself:
- Storage Blob Data Owner
- Storage Blob Data Contributor

## References
- [Copy acitivity Overview](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-overview)
- [Copy activity performance](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-performance)
- [Store credentials in AKV](https://learn.microsoft.com/en-us/azure/data-factory/store-credentials-in-key-vault)
- [Managed identity for ADF](https://learn.microsoft.com/en-us/azure/data-factory/data-factory-service-identity)
- [Constructing dynamic content](https://learn.microsoft.com/en-us/azure/data-factory/control-flow-expression-language-functions)
- [Scheduling with triggers](https://learn.microsoft.com/en-us/azure/data-factory/concepts-pipeline-execution-triggers#schedule-trigger-with-json)
