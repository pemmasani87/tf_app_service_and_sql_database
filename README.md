# tf_app_service_and_sql_database
Create Azure app service and sql server database using terraform and azure pipelines
Terraform configuration to provision an Azure Web App backed by an Azure SQL Database, with automated deployment via Azure Pipelines.

## Overview

This repository defines Infrastructure as Code (IaC) for the following Azure resources:

- **Resource Group** — logical container for all resources
- **App Service Plan** — hosting plan for the web app (Free/F1 tier)
- **Windows Web App** — the application hosting environment (.NET 8)
- **Azure SQL Server** — logical SQL server instance
- **Azure SQL Database** — the application database

The infrastructure is deployed and managed using Terraform, with pipeline automation handled through Azure Pipelines for consistent, repeatable deployments.

## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/downloads) >= 1.x
- An active Azure subscription
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) (for local authentication/testing)
- An Azure DevOps organization and project with Azure Pipelines enabled
- A Service Connection in Azure DevOps configured for your Azure subscription

## Repository Structure

tf_app_service_and_sql_database/
├── main.tf # Core resource definitions
├── providers.tf # Provider and backend configuration
├── variables.tf # Input variable declarations
├── outputs.tf # Output values (e.g., app URL, SQL server FQDN)
├── azure-pipelines.yml # CI/CD pipeline definition
├── .gitignore
└── README.md



## Getting Started (Local)

1. Clone the repository:
```bash
   git clone https://github.com/<your-username>/tf_app_service_and_sql_database.git
   cd tf_app_service_and_sql_database
```

2. Log in to Azure:
```bash
   az login
```

3. Initialize Terraform:
```bash
   terraform init
```

4. Review the execution plan:
```bash
   terraform plan
```

5. Apply the configuration:
```bash
   terraform apply
```

## CI/CD with Azure Pipelines

This repository includes an `azure-pipelines.yml` that automates:
- Terraform format and validation checks
- `terraform plan` on pull requests
- `terraform apply` on merge to `main`

Pipeline requires the following variables/secrets configured in Azure DevOps:
- `ARM_CLIENT_ID`
- `ARM_CLIENT_SECRET`
- `ARM_SUBSCRIPTION_ID`
- `ARM_TENANT_ID`

## Notes

- This project uses Free-tier (F1) SKUs where possible for cost-free testing/learning purposes.
- `always_on` is disabled in `site_config` since it is unsupported on the Free tier — expect cold starts after idle periods.
- Sensitive values (SQL admin credentials, etc.) should be supplied via pipeline secrets or Terraform variables, never hardcoded in `.tf` files.

## License

Specify a license here if applicable (e.g., MIT).
