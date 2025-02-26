# Lab 0: Setting up Azure Data Factory with Best Practices

## Objective
- Creating an ADF instance in Azure Portal
- Exploring the UI
- Configuring Git integration for source control

## Prerequisites
- Resource groups: rg-adfcourse-name-dev, rg-adfcourse-name-test
- Storage accounts (substitute with person name and resource group env):
  - dlsadfcoursenameenv001 (hierarchical namespace enabled)
  - dlsadfcourselognameenv001 (hierarchical namespace enabled)
  - stadfcoursesftpnameenv001 (SFTP enabled)
- Key vault: kv-adfcourse-name-env-001

## Steps

### 1. Create Storage Containers
- Create two containers in dlsadfcoursenamedev001:
  - inbound
  - outbound
- Create two containers in stadfcoursesftpnamedev001:
  - inbound
  - outbound

### 2. Upload Data
- Upload the provided [data package](./../data_package/) to outbound containers in dlsadfcoursenamedev001 and stadfcoursesftpnamedev001

### 3. Create ADF Instance
- Use Azure Portal to create a new Data Factory instance

### 4. Explore ADF UI
- Navigate through Author, Monitor, and Manage sections

### 5. Configure Git Integration
- Set up Git integration under manage for source control in ADF
