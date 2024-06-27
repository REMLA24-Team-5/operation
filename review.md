# Assignment 1
## Relevant links:
- operation: https https://github.com/REMLA24-Team-5/operation/tree/a1
- model-training: https://github.com/REMLA24-Team-5/Model-Training/tree/a1

## Comments:
Below we specify all the things we have implemented for each section. The model training repository contains all the code (link above).

### Project best practices: 
- we have split the code into different files and structed the repository using the data science template of cookie cutter
- Poetry allows for installation of the correct dependencies
- the dataset is automatically downloaded as part of the dvc pipeline
- exploratory code has been removed from python files and is only visible in the `notebooks` folder
- the README includes the steps as to how to use our repository
- all decisions are properly documented in the Readme.

### Pipeline Management:
- the pipeline can be run with `dvc repro`
- a remote storage has been configured using Google Drive
- DVC is used to report metrics and to keep track of different experiments/models
- Different metrics are reported beyond model correctness

### Code Quality
- The project follows code quality best practices
- Pylint yields a perfect score and was properly configured
- Configuration decisions follow ML conventions and are properly motivated in the Readme file
- Both dslinter (extension of pylint) and Bandit are configured and code quality information is displayed in the Readme
- In the Readme we critically analyse the linter rules, and propose changes that fit the ML project

<br></br>

# Assignment 2
## Relevant links:
- operation: https://github.com/REMLA24-Team-5/operation/tree/a2
- model-training: https://github.com/REMLA24-Team-5/Model-Training/tree/a2
- model-service: https://github.com/REMLA24-Team-5/model-service/tree/v0.0.10
- lib-ml: https://github.com/REMLA24-Team-5/lib-ml/tree/v0.1.2
- app: https://github.com/REMLA24-Team-5/app/tree/a2
- lib-version: https://github.com/REMLA24-Team-5/lib-version/tree/v0.1.5

## Comments:
Below we specify all the things we have implemented for each section.

### Data availability
#### Setup of the GitHub Organization
- The README contains all information to find and start the application

### Versioning and Releases
#### Automated Release Process
- All artifacts are released using the Git tag and automatically versioned
- The packaging and releases of all artifacts are performed in workflows.
- Release workflows automatically version all artifacts through using a Git release tag like v1.2.3
- Patch versions are automatically increased for both lib packages, bumps to minor or major versions remain manual

#### Software Reuse in Libraries
- Both libraries (`lib-ml` and `lib-version`) have been released such that they can be reused in other applications
- `lib-ml` contains meaningful data structures or logic that is used in both `model-training` and `model-service`
- The version string in lib-version is automatically updated with the actual package version in the release workflow, i.e., it is taken from the pyproject.toml file

### Containers and Orchestration
#### Exposing a Model via REST
- Flask is used to serve the model. A container image gets built and released in a workflow
- The model-service pre-processes queries the same was as in the training pipeline
- The model that is served can be updated without creating a new image, i.e., it is downloaded on-start
- All server endpoints have a well-defined API definition, created using Swagger

#### Sensible Use Case
- The app-service uses the model-service through REST. The microservice uses the version-aware lib-version through a package manager. The application has a basic frontend that allows to query the model
- The application asks the user whether he/she thinks it is phishing, this will allow for monitoring whether the model performs according to human expectations. This is on top of the basic query/response

#### Docker Compose Operation
- The operation repository contains a compose.yml file that allows to start up the application

<br></br>

# Assignment 3
## Relevant links:
- operation: https://github.com/REMLA24-Team-5/operation/tree/a3
- model-service: https://github.com/REMLA24-Team-5/model-service/tree/v0.1.7
- lib-ml: https://github.com/REMLA24-Team-5/lib-ml/tree/v0.1.2
- app: https://github.com/REMLA24-Team-5/app/tree/v0.0.5
- lib-version: https://github.com/REMLA24-Team-5/lib-version/tree/v0.1.5

## Comments:
Below we specify all the things we have implemented for each section.

### Provisioning
#### Setting up (Virtual) Infrastructure
- All levels have been implemented  

#### Setting up Software Environment
- The Kubernetes cluster has a controller and multiple (through a variable) registered nodes, which can be started from the host
- The playbook uses built-in modules to achieve idempotent provisioning
- Inventory and provisioning script differentiate between the control node and the worker nodes
- Inventory and/or provisioning script differntiate between the control node and worker nodes
- Prometheus, Grafana Dashboard are reachable, but the Kubernetes Dashboard is not implemented

### Kubernetes and Monitoring
#### Kubernetes Usage
- The application can be deployed to a Kubernetes cluster
- An Deployment.yml, Service.yml and Ingress.yml are present 
- A ConfigMap is used to store the model-service url
- Helm charts are not implemented

#### App monitoring
- Prometheus automatically collects many metrics about the app
- Metrics that are present include Gauge, Counter, Histogram and Summary
- A Prometheus Alertmanager is configured that raises an alert when more tahn 15 requests per minute are received for the last two minutes

#### Grafana
- An advanced dashboard is created, showing multiple different visualizations for the different metrics
- The dashboard is automatically installed
- The dashboard is not installed as part of a Helm chart

<br></br>

# Assignment 4
## Relevant links:
- model-training: https://github.com/REMLA24-Team-5/Model-Training/tree/a4-final

## Comments:
Below we specify all the things we have implemented for each section.

### Testing Framework 
- A testing framework is setup

### Automated Tests
- Thera are tests for non-determinism robustness and the use of data slices to test model capabilities
- There is a test for each of the following angles: Feature and Data; Model Development; ML infrastructure; Monitoring tests
- Model performance is being tested, also mutamorphic testing is present

### Continuous Training
- Pytest is automatically run when pushing, test statistics are stored but not automatically dispalayed in the README of the repository

<br></br>

# Assignment 5
## Relevant links:
- operation: https://github.com/REMLA24-Team-5/operation

## Comments:
Below we specify all the things we have implemented for each section.

### Traffic Management
- The system defines a Gateway and VirtualServices
- The project uses a DestinationRule and weights to enable a 90/10 routing of the app service
- Custom routing is not random. Repeated request from the same origin have a stable rating through specific user tokens in the request

### Continuous Experimentation
- The system deploys two versions of the app, with the button colors swapped. Metrics for both versions are collected to be able to check the change and decide whether the newer version is acceptable
- The report contains a section that describes the experiment

### Additional Use Case
- The shadow launch has been realized and is fully working
- The working use case is appropriately documented in the report

<br></br>

# Assignment 6
All rubric items for the report have been covered, and the report can be found in the repository.