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
        - after creation, check `Usage + quotas`, Standard NC Family vCPUs: should have 100+ available dedicated cores for this workshop (e.g., 5 people * 6 cores * 4 nodes = 120 cores)
    1. (optional) Add users in `Access Control (IAM)`
        - FYI: [Manage users and roles - create custom roles](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-assign-roles#create-custom-role)
    1. From Azure ML service Workspace `Overview` tab, click `Download config.json`, save locally.
    1. Set up Notebook environment. In this workshop, use Option 1 to practice.
        - Option 1: using Azure Notebooks
            - [Import the AML sample from GitHub](https://docs.microsoft.com/en-us/azure/notebooks/create-clone-jupyter-notebooks#import-a-project-from-github)
                - GitHub repo to import: https://github.com/Azure/MachineLearningNotebooks
                - private (if needed)
            - create a folder named `aml_config` at root of the imported project, upload the config.json file.
        - Option 2: using Notebook VMs from Azure ML service Workspace
            - go to `Notebook VMs`, create a new VM (STANDARD_D3_V2)
            - Click `JupyterLab`, click `Terminal`
            - From the current directory `/mnt/azmnt/code/Users/`, cd <USERNAME> (or mkdir if needed), git clone with `git clone https://github.com/Azure/MachineLearningNotebooks`
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/setup-notebook-vm-jupyterlab-gitclone.jpg)
            - Note that the config.json is already automatically added to `/mnt/azmnt/`, you do ***not*** need to upload it manually.
            - From `Notebook VMs`, click `Jupyter`, and you can run notebooks there
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/setup-notebook-vm-jupyter-notebook.jpg)

    1. Create Azure ML Compute: To do that, open `configuration.ipynb`

        - Skip creating config.json, because you already have it
        - Instead, add a cell and run following script to load the config.json and authenticate.
            ```python
            from azureml.core import Workspace
            ws = Workspace.from_config()
            ```
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/authenticate-workspace.jpg))
        - Proceed to create Azure ML Compute
            - `cpucluster` STANDARD_D2_V3, 0 to 4 nodes
            - `gpucluster` STANDARD_NC6, 0 to 4 nodes

- **11:00-11:50 Train first DL model on Notebook VM.**
    1. Open and run (before `run.wait_for_complettion()` cell) sample notebook `train-hyperparameter-tune-deploy-with-keras.ipynb` under `how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-keras` (find [this notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-keras/train-hyperparameter-tune-deploy-with-keras.ipynb) from your notebook environment)
    1. Monitor the Jupyter widget, and the Workspace (from Azure Portal - check Experiment and Compute)
    1. Additionally, note that files in `./outputs` and `./logs` are automatically uploaded to the Workspace. Tensorboard logs should also be saved in this `./logs`. Refer to [how to train models](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-train-ml-models#single-node-training) and [TensorBoard integration sample](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/tensorboard/tensorboard.ipynb).
    1. Try to understand how the model files are moving, from AML Compute, to Workspace, to local environment.
    1. Continue running the notebook and try hyperparameter tuning.
        - Set `max_concurrent_job` parameter to the maximum number of nodes in your Azure ML Compute cluster.
        - Run, monitor the Jupyter widget and Azure Portal (AML service Workspace), evaluate the results
            > Note: Generally when you open the Notebook, you can see the last run results of the code cells, but Jupyter widget results are not shown. So in order to review last Widget run status without running the experiment again, you should find and load the run before using the widget. Sample notebook to do this is [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/notebooks/Check-Jupyter-widget-for-a-specific-run.ipynb). 
    1. Stop here. You may continue and deploy to ACI, but we will cover this in the afternoon.

- **13:00-14:50 Distributed training with Horovod on AML Compute, explore AML Workspace.**

- **15:00-16:50 Create container images, deploy to Azure Container Instance, Azure Kubernetes Service**

- **17:00-17:50 Questions and answers**


