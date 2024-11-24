# Azure Services Experience

This document highlights my work with Azure services, including DevOps, infrastructure management, and cost optimization.

## Azure Services Used:
1. **Azure DevOps**:
   - Configured CI/CD pipelines using YAML.
   - Integrated automated testing and deployment workflows.

2. **Azure App Service**:
   - Deployed web applications using pipelines.
   - Configured scaling and monitoring for production readiness.

3. **Azure Kubernetes Service (AKS)**:
   - Deployed containerized applications to AKS.
   - Managed cluster nodes and monitored workloads.

4. **Azure Cost Management**:
   - Analyzed cost trends and optimized resource usage.
   - Configured budgets and alerts to monitor spending.

## Automation Scripts
Below are examples of scripts I used for Azure resource management:
- **PowerShell Script to Manage VMs**:
  ```powershell
  # Start a VM
  az vm start --name MyVM --resource-group MyResourceGroup
