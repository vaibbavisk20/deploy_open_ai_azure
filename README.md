# Deploy a Open AI Model to Azure Action

## Description

This GitHub Action automates the deployment of a sample Open AI Model. The action provisions the model along with any resources and roles it may need using azd commands.

In this model, we use a fictitious company called Contoso Electronics, and the experience allows its employees to ask questions about the benefits, internal policies, as well as job descriptions and roles.

**Currently, only works for subscriptions with OpenAI access**

[For more information on this template](https://github.com/Azure-Samples/azure-search-openai-demo)

**This documentation is for v1 of vaibbavisk20/deploy_open_ai_azure**

## Inputs

Please install the Azure OIDC app from the Github Marketplace to populate the below inputs as secrets in your repo

- **client-id** (required): Client ID used for Azure login.
- **tenant-id** (required): Tenant ID used for Azure login.
- **subscription-id** (required): Azure subscription ID used with the `az login`.
- **resource-group-name** (required): Resource group where Azure resources will be deployed.
- **location** (required): Location where Azure resources will be deployed.


## Usage

Create this workflow in your repo on this path: .github/workflows/workflow_file.yml

```yaml
name: Workflow to deploy Open AI Search Model on azure

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:

permissions:
  id-token: write
  contents: read

jobs:
  deploy-resources-to-azure:
    runs-on: ubuntu-latest
    steps:
        - name: Checkout master
          uses: actions/checkout@v3
          
        - name: Deploy a Open AI Model to Azure action
          uses: vaibbavisk20/deploy_open_ai_azure@v1
          with:
            client-id: ${{ secrets.AZURE_CLIENT_ID }}
            tenant-id: ${{ secrets.AZURE_TENANT_ID }}
            subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
            resource-group-name: ${{secrets.AZURE_RG}} 
            location: 'eastus'
```
## Output

The action creates an OpenAI model, the deployment can be viewed under the selected subscriptions deployments tab. Once the model is fully deployed, you can access the model UI using the displayed link in the workflow.
        
