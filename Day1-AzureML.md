# AMLWorkshop-IotEdge-DevOps
> ML/IoT/DevOps Hands on workshop

## Agenda
### Day 1 / 2019년 5월 15일(수)

#### 공통
- 09:30-10:00 Workshop overview, scope, expectations
  - Process flow and architecture [link(tbd)]()
  - DevOps pipeline [link(tbd)]()

#### ML Track
- **10:00-10:50 Dev environment setup: Azure ML service Workspace and Azure Notebooks. Authenticate, prepare compute (Azure ML Compute).**
  1. Install
    - [Visual Studio Code](https://code.visualstudio.com/)
    - [GitHub Desktop](https://desktop.github.com/)
    - (optional) Internet browser of your choice (Edge is fine, Chrome is also good)
  1. Check Azure subscription
    - All attendee should be able to sign in
  1. [Create an AML service workspace](https://docs.microsoft.com/en-us/azure/machine-learning/service/setup-create-workspace)
    - region: East US
    - resource group: new (one per person for practice)
    - after creation, check `Usage + quotas`, Standard NC Family vCPUs: should have 100+ available dedicated cores for this workshop (5 people * 6 cores * 2 nodes = 60 cores)
  1. (optional) Add users in `Access Control (IAM)`
    - FYI: [Manage users and roles - create custom roles](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-assign-roles#create-custom-role)
  1. From Azure ML service Workspace `Overview` tab, click `Download config.json`, save locally.
  1. Set up Notebook environment
    - Option 1: using Azure Notebooks
      - [Import the AML sample from GitHub](https://docs.microsoft.com/en-us/azure/notebooks/create-clone-jupyter-notebooks#import-a-project-from-github)
        - GitHub repo to import: https://github.com/Azure/MachineLearningNotebooks
        - private (if needed)
      - create a folder named `aml_config` at root of the imported project, upload the config.json file.
    - Option 2: using Notebook VMs from Azure ML service Workspace
      - go to `Notebook VMs`, create a new VM (STANDARD_D3_V2)
      - Click `JupyterLab`, click `Terminal`
        - cd or mkdir if needed, git clone with `git clone https://github.com/Azure/MachineLearningNotebooks`
          ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/setup-notebook-vm-jupyterlab-gitclone.jpg)
        - on the left pane, create a folder `aml_config` under `MachineLearningNotebooks`, upload the config.json from the Azure ML service Workspace
          ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/setup-notebook-vm-jupyterlab-upload-config.jpg)
       - From `Notebook VMs`, click `Jupyter`, and continue running notebooks
          ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/setup-notebook-vm-jupyter-notebook.jpg)
  1. Create Azure ML Compute: To do that, open `configuration.ipynb`
    - Skip creating config.json, because you already have it
    - Proceed to create Azure ML Compute
      - `cpucluster` STANDARD_D2_V3, 0 to 2 nodes
      - `gpucluster` STANDARD_NC6, 0 to 2 nodes

- **11:00-11:50 Train first DL model on Notebook VM.**
  1. Open and run sample notebook `train-hyperparameter-tune-deploy-with-keras.ipynb` under `how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-keras`

- **13:00-14:50 Distributed training with Horovod on AML Compute, explore AML Workspace.**

- **15:00-16:50 Create container images, deploy to Azure Container Instance, Azure Kubernetes Service**

- **17:00-17:50 Questions and answers**


