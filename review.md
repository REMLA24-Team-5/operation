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
- model service: https://github.com/REMLA24-Team-5/model-service/tree/a2
- lib-ml: https://github.com/REMLA24-Team-5/lib-ml/tree/a2
- app: https://github.com/REMLA24-Team-5/app/tree/a2
- lib-version: https://github.com/REMLA24-Team-5/lib-version/tree/a2

## Comments:
Below we specify all the things we have implemented for each section. The model training repository contains all the code (link above).

### Data availability
#### Setup of the GitHub Organization
- [TODO] the README contains all information to find and start the application

### Versioning and Releases
#### Automated Release Process
- All artifacts are released using the Git tag and automatically versioned 

#### Software Reuse in Libraries
- [TODO] Both libraries (`lib-ml` and `lib-version`) have been released such that they can be reused in other applications
- `lib-ml` is reused in both `model-training` and `model-service`

### Containers and Orchestration
#### Exposing a Model via REST
- [TODO]

#### Sensible Use Case
- [TODO]

#### Docker Compose Operation
- [TODO]
