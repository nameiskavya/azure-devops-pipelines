# Unified CI/CD Pipeline Documentation

## Overview
This repository demonstrates a **unified CI/CD pipeline** using **Azure DevOps** for both **Continuous Integration (CI)** and **Continuous Deployment (CD)**. 
The pipeline automates the process of building, testing, and deploying my application to **Azure App Service**. 
Below is an explanation of the different stages within this unified pipeline.

## Pipeline Stages

### 1. Build and Test (CI)
In this stage, the pipeline automatically builds the application and runs unit tests to ensure code quality.

#### Key Steps:
- **Trigger**: The pipeline is triggered automatically on changes to the `main` branch.
- **Tasks**:
  1. **Install Dependencies**: Install the necessary dependencies (e.g., using `npm` for JavaScript projects).
  2. **Run Tests**: Execute unit tests using a testing framework (e.g., Jest, Mocha).
  3. **Publish Test Results**: Store test results for reporting purposes.

#### Example YAML:
```yaml
trigger:
- master

pool:
  vmImage: ubuntu-latest

variables:
  buildConfiguration: 'Release'

steps:
- script: dotnet build --configuration $(buildConfiguration)
  displayName: 'dotnet build $(buildConfiguration)'
- task: DotNetCoreCLI@2
  displayName: 'Build MyWebSite'
  inputs:
    command: 'build'
- task: DotNetCoreCLI@2
  displayName: 'Publish MyWebSite'
  inputs:
    command: 'publish'
    publishWebProjects: true
- task: CopyFiles@2
  inputs:
    targetFolder: '$(Build.ArtifactStagingDirectory)' 
- task: PublishBuildArtifacts@1
  displayName: 'MyWebSiteArtifact'
  inputs:
    ArtifactName: 'MyWebSite'
    publishLocation: 'Container'
    PathtoPublish: '$(build.artifactstagingdirectory)'  
