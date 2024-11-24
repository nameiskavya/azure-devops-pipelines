# Azure Pipelines Documentation

## Overview
This repository contains a unified CI/CD pipeline for automating the build, test, and deployment of a sample application using **Azure DevOps**.

### CI/CD Workflow
The pipeline performs the following steps:
1. **Continuous Integration (CI):** 
   - Builds the application.
   - Runs automated tests.
   - Publishes the results.
2. **Continuous Deployment (CD):** 
   - Deploys the tested application to **Azure App Service**.

### YAML Configuration
The entire workflow is defined in the `azure-pipelines.yml` file.

#### Key Pipeline Stages:
1. **Build and Test**:
   - Installs dependencies.
   - Runs unit tests and publishes results.
   - Example:
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
		

![Screenshot](screenshots/azure-pipeline.png)
![Screenshot](screenshots/azure releases.png)

