# Azure DevOps Pipeline with GitHub

This repository contains an Azure DevOps pipeline that automates the build, test, and deployment process for a project hosted on GitHub.

## 🚀 Getting Started

### 1️⃣ Prerequisites
- An **Azure DevOps** account ([Sign up](https://dev.azure.com/))
- A **GitHub** repository with your source code
- Admin access to configure pipeline permissions

### 2️⃣ Setting Up the Pipeline

#### Step 1: Connect GitHub to Azure DevOps
1. Go to **Azure DevOps** and navigate to your project.
2. Click **Pipelines** > **New pipeline**.
3. Select **GitHub** as the source repository.
4. Authorize Azure DevOps to access your GitHub repo.
5. Choose your repository and continue.

#### Step 2: Define the YAML Pipeline

Create an `azure-pipelines.yml` file in your repository root:

```yaml
trigger:
- main  # Runs when code is pushed to 'main'

pool:
  vmImage: 'ubuntu-latest'  # Use an Ubuntu-based agent

steps:
- task: UseNode@1
  inputs:
    version: '16.x'  # Install Node.js 16

- script: |
    npm install
    npm run build
  displayName: 'Install dependencies and build'

- script: |
    npm test
  displayName: 'Run tests'

- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: '$(Build.ArtifactStagingDirectory)'
    artifactName: 'drop'
