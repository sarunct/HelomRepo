Generic Helm Chart for Python-based ML API

This repository contains a generic Helm chart designed to deploy a Python-based Machine Learning (ML) API. The chart is configured to support three environments: development, staging, and production. This document provides step-by-step instructions on how ML engineers can reuse this chart for their own projects.

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

Each file allows for environment-specific configurations, making it easier to manage differences in resources, scaling, and service settings across development, staging, and production environments. Also Ensures that the same Helm chart can be used across different stages of development, with only the necessary configuration changes for each environment.

It also simplifies the deployment process by allowing engineers to switch between environments without modifying the core Helm chart, just by selecting the appropriate values file.

How to use the chart to deploy your ML API:

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

Deployment Process:

Once you have made changes to the values file, push the changes to your own repository to deploy your API in Kubernetes cluster.

1, Repository - Create a new or push you change you the existing repository for deployment.

      git add values/<environment>.yaml
      git commit -m "update values for <environment> deployment"


2, Push to Your Repository

    git push origin <branch_name>

Triggering Deployment Pipeline:

  Pushing changes to your repository will trigger the deployment pipeline configured in your CI/CD system. This pipeline will automatically deploy the updated configuration to your Kubernetes cluster.

Kubernetes Cluster:

  Kubernetes URL - 
  How to access you cluster - 
  How to check the logs - 


