# AMLWorkshop-IotEdge-DevOps
> ML/IoT/DevOps Hands on workshop

## Agenda
### Day 1

#### 공통
- 09:30-10:00 Workshop overview, scope, expectations
  - Process flow and architecture ([pdf](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/doc/decks/Microsoft%20AI%20Architecture%20one-slider-EN-v20190513.pdf))
  - DevOps pipeline ([pdf](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/doc/decks/DevOps-ML-IotEdge-pipeline-flow-v20190513.pdf))


#### ML Track
- **10:00-10:50 Dev environment setup: Azure ML service Workspace and Azure Notebooks, authenticate, prepare compute (Azure ML Compute)**

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

- **11:00-11:50 Train first DL model on Azure Notebooks using Azure ML Compute**

    1. Open sample notebook `train-hyperparameter-tune-deploy-with-keras.ipynb` under `how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-keras` (find [this notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-keras/train-hyperparameter-tune-deploy-with-keras.ipynb) from your notebook environment)
    1. Run (before `run.wait_for_complettion()` cell)
    1. Monitor the Jupyter widget, and the Workspace (from Azure Portal - check Experiment and Compute)
    1. Additionally, note that files in `./outputs` and `./logs` are automatically uploaded to the Workspace. Tensorboard logs should also be saved in this `./logs`. Refer to [how to train models](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-train-ml-models#single-node-training) and [TensorBoard integration sample](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/tensorboard/tensorboard.ipynb).
    1. Try to understand how the model files are moving, from AML Compute, to Workspace, to local environment.
    1. Continue running the notebook and try hyperparameter tuning.
        - Set `max_concurrent_job` parameter to the maximum number of nodes in your Azure ML Compute cluster.
        - Run, monitor the Jupyter widget and Azure Portal (AML service Workspace), evaluate the results
            > Note: Generally when you open the Notebook, you can see the last run results of the code cells, but Jupyter widget results are not shown. So in order to review last Widget run status without running the experiment again, you should find and load the run before using the widget. Sample notebook to do this is [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/notebooks/Check-Jupyter-widget-for-a-specific-run.ipynb). 
    1. Stop here. You may continue and deploy to ACI from this notebook, but we will cover deployment in the afternoon.

- **13:00-14:50 Distributed training with Horovod on AML Compute, explore AML Workspace**

    1. Open sample notebook `distributed-pytorch-with-horovod.ipynb` under `how-to-use-azureml/training-with-deep-learning/distributed-pytorch-with-horovod` (find [this notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/distributed-pytorch-with-horovod/distributed-pytorch-with-horovod.ipynb) from your notebook environment)
    1. Run all: consider using 4 nodes when available instead of 2 as `node_count`.
    1. Questions and answers, or proceed to the next step.

- **15:00-16:50 Create container images, deploy to Azure Container Instance (and/or Azure Kubernetes Service)**

    1. We will continue from morning's sample, `train-hyperparameter-tune-deploy-with-keras.ipynb`. Open the notebook, and run the latter part, creating container image and deploying to ACI.
    1. Explore Workspace from Azure Portal.
    1. Refresh the concepts of MLOps from [concept-model-management-and-deployment](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-model-management-and-deployment)

    * If time permits, try below contents in addition:

        - [Build 2019 updates](https://azure.microsoft.com/en-us/blog/new-azure-machine-learning-updates-simplify-and-accelerate-the-ml-lifecycle/): New Azure Machine Learning updates simplify and accelerate the ML lifecycle
        - [visual-interface (preview)](https://docs.microsoft.com/en-us/azure/machine-learning/service/ui-tutorial-automobile-price-train-score)
        - [automated ml with GUI (preview)](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-create-portal-experiments)
        - [interpretability-explainability](https://docs.microsoft.com/en-us/azure/machine-learning/service/machine-learning-interpretability-explainability)
        - [onnx](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-onnx)
        - [fpga](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-accelerate-with-fpgas)
        - [pipelines](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-ml-pipelines)
        - [security](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-enterprise-security)
        - [custom vision](https://customvision.ai)

    * Running AML SDK on Azure Databricks
        - Set up Azure Databricks using this [guide](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-configure-environment#azure-databricks)
        - Create a cluster, and import the [sample notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/azure-databricks/Databricks_AMLSDK_1-4_6.dbc).
        - Install `azureml-sdk[automl_databricks]` if needed.
        - Run samples.
            - For Automated ML sample, set `max_concurrent_iterations` to the number of worker nodes.

    * And check out [MLOps](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-model-management-and-deployment). This will be covered in Day 3, but will be good if we can get familiar with key concepts earlier.

- **17:00-17:50 Questions and answers**


