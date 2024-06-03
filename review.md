# Assignment 1
## Relevant links:
- operation: https https://github.com/REMLA24-Team-5/operation/tree/a1
- model training: https://github.com/REMLA24-Team-5/Model-Training/tree/a1

## Comments:
Below we specify all the things we have implemented for each section. The model training repository contains all the code (link above).

### Project best practices: 
- we have split the code into different files and structed the repository using the data science template of cookie cutter
- Poetry allows for installation of the correct dependencies.
- the dataset is automatically downloaded as part of the dvc pipeline
- exploratory code has been removed from python files and is only visible in the `notebooks` folder
- the README includes the steps as to how to use our repository
- all decisions are properly documented in the Readme.

### Pipeline Management:
- the pipeline can be run with `dvc repro`
- a remote storage has been configured using Google Drive
- DVC is used to report metrics and to keep track of different experiments/models.
- Different metrics are reported beyond model correctness

### Code Quality
- The project follows code quality best practices
- Pylint yields a perfect score and was properly configured.
- Configuration decisions follow ML conventions and are properly motivated in the Readme file
- Both dslinter (extension of pylint) and Bandit are configured and code quality information is displayed in the Readme
- In the Readme we critically analyse the linter rules, and propose changes that fit the ML project

# Assignment 2
## Relevant links:
- operation: https://github.com/REMLA24-Team-5/operation/tree/a2
- model training: https://github.com/REMLA24-Team-5/Model-Training/tree/a2
- model service: https://github.com/REMLA24-Team-5/model-service/tree/v0.0.10
- lib-ml: https://github.com/REMLA24-Team-5/lib-ml/tree/v0.1.2
- app: https://github.com/REMLA24-Team-5/app/tree/a2
- lib-version: https://github.com/REMLA24-Team-5/lib-version/tree/v0.1.5

## Comments:
Below we specify all the things we have implemented for each section.

### Data availability
#### Setup of the GitHub Organization
- The README contains all information to find and start the application, however the docker compose up fails as the connection to the model-service image is not finalized.

### Versioning and Releases
#### Automated Release Process
- All artifacts are released using the Git tag and automatically versioned
- The packaging and releases of all artifacts are performed in workflows.
- Release workflows automatically version all artifacts through using a Git release tag like v1.2.3.
- Patch versions are automatically increased for both lib packages, bumps to minor or major versions remain manual.

#### Software Reuse in Libraries
- Both libraries (`lib-ml` and `lib-version`) have been released such that they can be reused in other applications
- `lib-ml` contains meaningful data structures or logic that is used in both `model-training` and `model-service`
- The version string in lib-version is automatically updated with the actual package version in the release workflow, i.e., it is taken from the pyproject.toml file.

### Containers and Orchestration
#### Exposing a Model via REST
- Flask is used to serve the model. A container image gets built and released in a workflow.
- The model-service pre-processes queries the same was as in the training pipeline.
- The model that is served can be updated without creating a new image, i.e., it is downloaded on-start.

#### Sensible Use Case
- The app-service uses the model-service through REST. The microservice uses the version-aware lib-version through a package manager. The application has a basic frontend that allows to query the model (”a textbox with a button”) but it fails in showing the result for now.

#### Docker Compose Operation
- The operation repository contains a docker-compose.yml file that allows to start up the application and use it but it does not work for now.

# Assignment 3
## Relevant links:
- operation: https://github.com/REMLA24-Team-5/operation/tree/a3
- model training: https://github.com/REMLA24-Team-5/Model-Training/tree/a2
- model service: https://github.com/REMLA24-Team-5/model-service/tree/v0.1.7
- lib-ml: https://github.com/REMLA24-Team-5/lib-ml/tree/v0.1.2
- app: https://github.com/REMLA24-Team-5/app/tree/v0.0.5
- lib-version: https://github.com/REMLA24-Team-5/lib-version/tree/v0.1.5

## Comments:
Below we specify all the things we have implemented for each section.

### Provisioning
#### Setting up (Virtual) Infrastructure
- All levels have been implemented  

#### Setting up Software Environment
- The Kubernetes cluster can be started from withing the controller (vagrant ssh controller), however the cluster does not work 
- The playbook uses built-in modules to achieve idempotent provisioning
- Inventory and provisioning script differentiate between the control node and the worker nodes
- Prometheus, Grafana and Kubernetes Dashboard are not yet reachable

### Kubernetes and Monitoring
#### Kubernetes Usage
- So far the Kubernetes cluster is not working yet
- An Deployment.yml, Service.yml and Ingress.yml are present 
- A ConfigMap is used to store the model-service url
- Helm chart is not there

#### App monitoring
- Nothing has been implemented yet

#### Grafana
- Nothing has been implemented yet

# Assignment 4
## Relevant links:
- model training: https://github.com/REMLA24-Team-5/Model-Training/tree/a4-final

## Comments:
Below we specify all the things we have implemented for each section.

[//]: # (This is not really under the right categories)
#### Testing Framework 
- We have configured pytest to test all components within the repository, this includes getting data, preprocessing and model definition.
- We want to increase test coverage for the final submission
#### Automated Tests
- Pytest is automatically run when pushing, test statistics are not yet pushed automatically

# Assignment 5
## Relevant links:

## Comments:
We did not implement anything for this assignment as we are still stuck on past assignments.