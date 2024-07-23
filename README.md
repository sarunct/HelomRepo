Generic Helm Chart for Python-based ML API & Branching Strategy 

This repository contains a generic Helm chart designed to deploy a Python-based Machine Learning (ML) API and the Branching Strategy. The chart is configured to support three environments: development, staging, and production. This document provides step-by-step instructions on how ML engineers can reuse this chart for their own projects.

Chart Structure:

    mf-demo
    ├── Chart.yaml
    ├── README.md
    ├── charts
    ├── environment
    │   ├── dev
    │   │   └── value-dev.yaml
    │   ├── production
    │   │   └── value-production.yaml
    │   └── staging
    │       └── value-staging.yaml
    ├── index.yaml
    └── templates
        ├── NOTES.txt
        ├── _helpers.tpl
        ├── deployment.yaml
        ├── service.yaml
        ├── serviceaccount.yaml
        └── tests
            └── test-connection.yaml

    charts/: Contains the Helm chart files.
    enviroment/: Contains environment-specific values files.
          values-dev.yaml: Configuration for the Development environment.
          values-staging.yaml: Configuration for the Staging environment.
          values-production.yaml: Configuration for the Production environment.

  The char contains the yaml file for creating the kubernets object. Also it has three different value files value-dev.yaml, value-staging.yaml and value-production.yaml.

  Each file allows for environment-specific configurations, making it easier to manage differences in resources, scaling, and service settings across development, staging, and production environments. Also Ensures that the 
  same Helm chart can be used across different stages of development, with only the necessary configuration changes for each environment.

  It also simplifies the deployment process by allowing engineers to switch between environments without modifying the core Helm chart, just by selecting the appropriate values file.

**How to use the chart to deploy your ML API:**

   Deployment Process:
   1, To deploy the Python-based ML API using this Helm chart, follow these steps:
  
   Clone the Repository -
      
        git clone <repository-url>
        cd <repository-directory>

  
   2, Update the appropriate values file based on your target environment:
  
   values-dev.yaml for Development
   values-staging.yaml for Staging
   values-production.yaml for Production
  
   Edit the values files to fit your specific configuration needs. 
      
      For example -
      
      image:
        repository: my-python-api
        tag: latest
        
   Customize the values-<environment>.yaml files to specify different settings for your deployment. Key areas to customize include:
  
      Image Repository and Tag - Specify the Docker image repository and tag for the Python API.
      Replicas - Set the number of replicas for scaling.
      Resource Limits - Define CPU and memory limits.

**Deployment Process:**

  Once you have made changes to the values file, push the changes to your own repository to deploy your API in Kubernetes cluster.

  1, Repository - Create a new or push you change you the existing repository for deployment.

      git add values/<environment>.yaml
      git commit -m "update values for <environment> deployment"


  2, Push to Your Repository

    git push origin <branch_name>

**Triggering Deployment Pipeline:**

  Pushing changes to your repository will trigger the deployment pipeline configured in your CI/CD system. This pipeline will automatically deploy the updated configuration to your Kubernetes cluster.

  Kubernetes Cluster:

  Kubernetes URL - 
  How to access you cluster - 
  How to check the logs - 

**Branching Strategy:**

  To manage Helm charts repository, a clear and effective branching strategy is imporant to maintaining stability, promoting changes, and to support various environments. Here’s a recommended branching strategy for your 
  Helm chart repository

  master: This branch contains the stable, production version of the Helm chart. Changes are only merged into this master branch from release branch

  release: This branch contains the stable, production-ready version of the Helm chart. Changes are only merged into this release branch after multiply stages testing and review.

  develop: This branch is used for integrating feature developments and testing. It reflects the latest development work and is usually deployed to a staging environment for testing before merging into main.

Environment-Specific Branches:

  dev: This branch is dedicated to development-specific changes. It might be used to deploy to a development environment for initial testing and validation.
    
  staging: This branch is used for staging environment changes. It serves as a pre-production environment for final testing before merging into main.
    
  production: This branch, if used, should mirror the main branch and be used to manage production-specific configurations or fixes.

Feature Branches:

  feature/<feature-name>: Create a new branch for each feature or change you’re working on. These branches are based off of develop or the relevant environment branch, and are merged back into develop or the environment 
  branch after the feature is complete and tested.
  
Release Branches:

  release-<release version>: When preparing for a release, create the release branch from master . Use this branch for final testing, bug fixes, and document the change, This branch will be deployed to the production environment, Once the produciton validationg is compelted successfull and got confirmation form users merge the release brnach to the master branch.

Hotfix Branches:

  hotfix/<issue>: For urgent fixes that need to be applied to the production environment, create a hotfix branch from main. Once the hotfix is complete, merge it into main and develop (or the relevant environment branches).
