# Lab 4: CI/CD Pipeline Deployment

## Objective
Implement cross-environment deployment

## Points Covered
- The Published artifact
- Global Parameters
- ARM Parametrization
- Pre/post-deployment scripts: Disabling triggers, deleting old resources

## Steps

### 1. Create Global Parameter and prepare for CI/CD
- Create global parameter
- Go into ARM template and check "include global parameter in ARM template"
- Update linked services, datasets, and pipelines with the global parameter
- Copy dataset to outbound container in SFTP and DLS in test resource group

### 2. Setup CI/CD

#### GitHub
1. Register service principal
2. Give service principal contributor access on resource groups
3. Generate client secret
4. Add secret in GitHub with the following format:
```
{
"clientId": "<Client ID>",
"clientSecret": "<Client Secret>",
"subscriptionId": "<Subscription ID>",
"tenantId": "<Tenant ID>"
}
```

5. Copy code from repo
6. Make pull request, ensure CI completes before merging

#### Azure DevOps
1. Create starter pipeline with YAML from [this](https://learn.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery-improvements#create-an-azure-pipeline), dont forget to also save the package.json in a folder called something like “automation_build” or similar
3. Enable classic release pipelines in project settings
4. Create release pipeline (empty job)
5. Add pipeline variables for resource group and Azure Data Factory
6. In the pipeline add artifact targeting the build pipeline

##### Configure Release Pipeline
1. Add Azure PowerShell task for pre-deployment script (PrePostDeploymentScript.ps1), then use the predeployment arguments from [this](https://learn.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery-sample-script) and replace the placeholders. Under advanced tick use PowerShell core
2. Add ARM template deployment task. Authorize it only for the dev resource group. Select Action: create or update. *IMPORTANT* Deployment Mode = incremental if it is complete it will *DELETE EVERYTHING* in the resource group that is not part of the arm template.
3. Add Azure PowerShell task for post-deployment script using the same script and the other arguments at the link in 1
4. Configure continuous deployment trigger

##### Clone and Customize for Test Environment
- Go and give the service principal, found under linked services, the contributor role for the test resource group as well
- Clone the stage
- Update resource groups and data factory references to test
- Override template parameters
    - substitute factoryName with variable and environment. 
    - Additionally, override the global parameter default_properties_environment_value (It can be that this will not work in which case you will have to provide another powershell script before armtemplate deployment to change the global parameter with the GlobalParametersUpdateScript.ps1, using the arguments defined [here](./../.github/actions/CD/action.yml))

## References
- [Continuous integration and delivery in Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery)
- [Create an Azure pipeline](https://learn.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery-improvements#create-an-azure-pipeline)
- [Sample deployment scripts](https://learn.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery-sample-script)
