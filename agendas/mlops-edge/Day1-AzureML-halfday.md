# Azure ML half-day Workshop
> Shorter version of AzureML Hands on workshop

## Scope

- 4시간 짜리 요약 버전으로 핵심 내용 위주로 진행합니다.
- Azure에 데이터를 올리는 가장 간단한 방법부터 시작해서, Azure ML workspace를 생성하고 첫 실험을 수행하는 부분, Azure ML의 주요 기능 중에서 선별하여 실습 또는 데모를 통해 체험을 합니다.
- Inference 부분은 시간이 부족하여 MLOps 관점에서 데모 중심으로 커버합니다.
- 본 버전에서는 Client에 설치를 최소화하고 Cloud 환경에서 대부분의 작업을 진행합니다.
- 본 세션으로 Azure ML의 모든 것을 알 수는 없으나 최소한의 개념을 일부라도 직접 체험하고 향후에 기능별로 알아보기 위한 기초를 마련하도록 합니다.
- 시간이 허용된다면 고급 기능의 일부를 알아봅니다:
  - Experiment e2e tracking
  - Automated ML, HyperDrive
  - MLOps
  - Distributed Training with SR-IOV
  - DeepSpeed
  - Enterprise Readiness

## Agenda

### Before the session

- Prepare

    1. Check Azure subscription
        - All attendee should be able to sign in
    1. Install
        - Internet browser of your choice (Edge is fine, Chrome is also good)
        - [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/)
            1. 설치 후 Azure Storage Explorer를 실행하고 왼쪽 상단의 사람모양 아이콘 클릭 후 `Add an account` 클릭
                ![storage-explorer-add-account1](./doc/images/storage-explorer-add-account1.jpg)
            1. `Add an Azure Account` 선택 후 `Next` 클릭
                ![storage-explorer-add-account2](./doc/images/storage-explorer-add-account2.jpg)
            1. Azure 계정으로 로그인
            1. 로그인 후 계정 연동 확인
                ![storage-explorer-add-account3](./doc/images/storage-explorer-add-account3.jpg)
        - (optional) [Visual Studio Code](https://code.visualstudio.com/)
        - (optional) [GitHub Desktop](https://desktop.github.com/)

### Day 1 (Half)

#### Basic

- **14:00-14:50 Workshop overview, scope, expectations and getting started**

    1. [Create an AML service workspace](https://docs.microsoft.com/en-us/azure/machine-learning/service/setup-create-workspace)
        - region: Korea Central
        - resource group: new (one per person for practice)
        - after creation, check `Usage + quotas`, Standard NC Family vCPUs: should have enough available dedicated cores for this workshop (e.g., 5 people * 6 cores * 4 nodes = 120 cores), if we're trying Deep Learning
    1. (optional) Add users in `Access Control (IAM)`
        - FYI: [Manage users and roles - create custom roles](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-assign-roles#create-custom-role)
    1. Use [Storage Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) to upload files
        - Note it leverages [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) for parallel faster loading
    1. Key concepts
        - Data flow and architecture ([pdf](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/doc/decks/Microsoft%20AI%20Architecture%20one-slider-EN-v20190513.pdf))
            - [Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/)
                - [AWS S3 connector](https://docs.microsoft.com/en-us/azure/data-factory/connector-amazon-simple-storage-service)
        - (Optional) DevOps pipeline ([pdf](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/doc/decks/DevOps-ML-IotEdge-pipeline-flow-v20190513.pdf))
        - Azure ML Overview "AI 프로젝트에 필요한 것들"
        - Azure ML [conceptual diagram](https://docs.microsoft.com/en-us/azure/machine-learning/concept-workspace)

#### Drilling down

- **15:00-15:50 Visit AML studio, create computes and try Notebooks**

    1. visit https://ml.azure.com/ or https://ml.azure.com?flight=azureNotebooks
    1. Learn key concepts
    1. [Create Compute Instance](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-environment#compute-instance). Or alternatively you can [use your local environment](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-environment#local).
        - Go to `Compute` > `Compute Instance`, create a new VM (STANDARD_D3_V2)
        - Clone sample git repo. Choose one of the following options.
            - Option 1: Use GUI
                1. You can do this even if you don't have Compute Instance running.
                1. Go to `Notebooks`, drill down `Azure ML gallery` - `Samples`. Choose any folder you want to clone, click `...` of that folder and choose `Clone`.
                ![setup-computeinstance-gitclone](./doc/images/setup-computeinstance-gitclone-ui.jpg)
            - Option 2: Use code
                1. You can do this only when your Compute Instance is running.
                1. Go to `Compute` > `Compute Instance`. Start the Compute Instance if it is not running. Click `JupyterLab` of a running Compute Instance, click `Terminal`
                1. From the home directory `/mnt/azureuser/`, cd <USERNAME> (or mkdir if needed, name can by anything you want), git clone with `git clone https://github.com/Azure/MachineLearningNotebooks`
                ![setup-computeinstance-jupyterlab-gitclone](./doc/images/setup-computeinstance-jupyterlab-gitclone.jpg)
    1. Run Notebooks from the cloud
        - You have two ways to do this. Choose one of the following options. Both requires running Compute Instance.
        - Option 1: Use studio (UI)
            1. Go to `Notebooks` > `User files`, choose the Jupyter Notebook you want to run.
            1. If no Compute Instance is running, you can start it from `Compute` > `Compute Instance` and come back here.
                ![setup-computeinstance-start-stop](./doc/images/setup-computeinstance-start-stop.jpg)
            1. You can specify on which Compute Instance you will run the Notebook.
                ![setup-computeinstance-run-notebook-ui](./doc/images/setup-computeinstance-run-notebook-ui.jpg)
            1. You can edit, run and document as you would normally do with Jupyter Notebook. 
        - Option 2: Use Compute Instance Jupyter directly
            1. From `Compute` > `Compute Instance`, click `Jupyter`, and you can run notebooks there
            ![setup-computeinstance-jupyter-notebook-run](./doc/images/setup-computeinstance-jupyter-notebook-run.jpg)
    1. (Optional) In case you want to skip AD authentication and use SSH Tunneling to access services running in the Compute Instance such as Jupyer:
        1. Create SSH Key pair using PuTTYgen or any other tools. If you use PuTTYgen,
            1. Run `bash`
            1. Install PuTTYgen if you haven’t, by running `sudo apt install putty-tools`.
            1. Run the following command to generate the key pair, save the Private Key, then retrieve the Public Key in OpenSSH rsa format which is needed for Compute Instance creation.

                ```bash
                puttygen -t rsa -b 2048 -C "azureuser@ci" -o private-key.ppk
                puttygen private-key.ppk -O public-openssh -o public-key-openssh
                ```

                > If you wanted to set passphrase, refer to the documentation shared above.

        1. Create Compute Instance using SSH Public Key above
        1. Use PuTTY or any other tools to create SSH Tunnel between localhost and remote Compute Instance
        1. Now you can browse [https://localhost:8000/](https://localhost:8000/) to get to Jupyter (and [https://localhost:8000/lab](https://localhost:8000/lab) for JupyterLab) running remotely in Compute Instance.

    1. Create Azure ML Compute: To do that, open `configuration.ipynb` under Notebooks

        - Proceed to create Azure ML Compute
            - `cpucluster` STANDARD_D2_V3, 0 to 4 nodes
            - `gpucluster` STANDARD_NC6, 0 to 4 nodes

    1. Try a Notebook: [sample - first ml experiment](https://github.com/Azure/MachineLearningNotebooks/tree/master/tutorials/create-first-ml-experiment)

- **16:00-16:50 Try Automated ML**

    1. (Demo) Regression example
        1. Open sample notebook `auto-ml-regression-hardware-performance-explanation-and-featurization` under `how-to-use-azureml/automated-machine-learning/regression-hardware-performance-explanation-and-featurization` (find [this notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/automated-machine-learning/regression-hardware-performance-explanation-and-featurization/auto-ml-regression-hardware-performance-explanation-and-featurization.ipynb) from your notebook environment)
        1. Run (before `run.wait_for_complettion()` cell)
        1. Monitor the Jupyter widget, and the Workspace (from Azure Portal - check Experiment and Compute)
        1. Additionally, note that files in `./outputs` and `./logs` are automatically uploaded to the Workspace. Tensorboard logs should also be saved in this `./logs`. Refer to [how to train models](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-train-ml-models#single-node-training) and [TensorBoard integration sample](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/tensorboard/tensorboard.ipynb).
        1. Try to understand how the model files are moving, from AML Compute, to Workspace, to local environment.
    1. (Your turn) Let's try Regression with UI
        1. Upload the [sample orage juice CSV](./sample/dominicks_OJ.csv)
            - Option 1: Use Storage Explorer to upload data to Storage Account attached to Azure Machine Learning
            - Option 2: Use Azure ML studio > `Datasets` > `Create dataset`. Check header. Try Profile and Explore.
                ![upload-data-azureml-dataset](./doc/images/upload-data-azureml-dataset.jpg)
                ![upload-data-azureml-dataset1](./doc/images/upload-data-azureml-dataset1.jpg)
                ![upload-data-azureml-dataset2](./doc/images/upload-data-azureml-dataset2.jpg)
                ![upload-data-azureml-dataset3](./doc/images/upload-data-azureml-dataset3.jpg)
                ![upload-data-azureml-dataset4](./doc/images/upload-data-azureml-dataset4.jpg)
        1. Go to `Automated ML`, click `New Automated ML run` and try regression.
            1. Pick the dataset you uploaded, pick target column.
            1. Choose the Compute you have created (e.g., CPU cluster)
            1. Choose `Regression` if that is what you want to run.
            1. Check out `View feaurization settings`
            1. Check out `View additional configuration settings`
                - Primary Metrics
                - Automatic Featurization
                - Explain best model
                - Blocked algorithms
                - Exit criterion
                - Validation
                - Concurrency
            1. Click Submit
            1. Check `Automated ML` (Data guadrails, Models), `Experiments`, `Compute`
            1. Check `Explainer`
            1. You may try `Deploy best model` from the run.

- **17:00-17:50 Check out Designer and MLOps**

    1. Designer
        1. Try starting a new Pipeline Draft
        1. Try opening a sample
        1. Check out quick demos
    1. [MLOps](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-model-management-and-deployment)
        1. Revist the architecture diagram
        1. Check out quick demos
            1. [Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/?name=azure%20machine%20learning)
    1. Some more additional features
        - [Build 2019 updates](https://azure.microsoft.com/en-us/blog/new-azure-machine-learning-updates-simplify-and-accelerate-the-ml-lifecycle/): New Azure Machine Learning updates simplify and accelerate the ML lifecycle
        - [visual-interface (preview)](https://docs.microsoft.com/en-us/azure/machine-learning/service/ui-tutorial-automobile-price-train-score)
        - [automated ml with GUI (preview)](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-create-portal-experiments)
        - [interpretability-explainability](https://docs.microsoft.com/en-us/azure/machine-learning/service/machine-learning-interpretability-explainability)
        - [onnx](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-onnx)
        - [fpga](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-accelerate-with-fpgas)
        - [pipelines](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-ml-pipelines)
        - [Enterprise Readiness](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-enterprise-security)
        - [Distributed Training with SR-IOV](https://techcommunity.microsoft.com/t5/azure-ai/accelerating-distributed-training-in-azure-machine-learning/ba-p/1059050)
        - [DeepSpeed](https://www.microsoft.com/en-us/research/blog/zero-deepspeed-new-system-optimizations-enable-training-models-with-over-100-billion-parameters/)
        - [Model Inference Optimization (private)](https://github.com/Azure/ModelInferenceOptimization#model-inference-optimization-workflow-and-hidden-tech)
        - [custom vision](https://customvision.ai)
    1. Further questions
