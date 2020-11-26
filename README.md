# AMLWorkshop-IotEdge-DevOps
> This repo caters different scenarios regarding Azure ML workshops

- [Agenda: Many Models with Azure ML](#agenda-many-models-with-azure-ml)
- [Agenda: ML/IoT/DevOps Hands on Workshop](#agenda-mliotdevops-hands-on-workshop)

---

## Agenda: Many Models with Azure ML

### Day 1: AutoML and Pipelines Basic - full instructions [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/agendas/many-models/Day1-automl-pipeline-basic.md)

- Pre-requisites
  - Python skills
  - Understanding of [key concepts of Azure ML](https://docs.microsoft.com/en-us/azure/machine-learning/concept-azure-machine-learning-architecture)
  - Get familiar with Azure ML by running other experiments, trying own datasets, extending from previous workshops
  - Bring any questions on overall Azure ML, share your feedbacks so far before Day 1

- Morning
  - Intro to agenda, getting to know each other
  - Fundamentals
  - Discussions

- Afternoon
  - Automated ML
  - ML Pipeline
  - Discussions

### Day 2: Dive into Many Models - full instructions [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/agendas/many-models/Day2-dive-into-many-models.md)

- Pre-requisites
  - Full understanding of key concepts on [ML Pipelines](https://docs.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines)
  - Watch videos ([1](https://channel9.msdn.com/Shows/Docs-AI/Building-Large-Scale-Machine-Learning-Forecasting-Models-using-Azure-Machine-Learnings-Automated-ML), [2](https://channel9.msdn.com/Shows/Docs-AI/Building-Large-Scale-Machine-Learning-Models-using-Azure-Machine-Learning), less than 30 min in total) on the solution accelerator for many models
  - Bring any questions on Pipeline before Day 2
  - (Optional) Create SSH key pairs (OpenSSH rsa format) and install [VSCode](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-set-up-vs-code-remote) for remote connection

- Morning
  - Intro to [SA for many models](https://github.com/microsoft/solution-accelerator-many-models)
  - Set up dev env (new compute instance, conda env, optional: vscode remote connection)
  - Recap [ParallelRunStep](https://docs.microsoft.com/en-us/python/api/azureml-pipeline-steps/azureml.pipeline.steps?preserve-view=true&view=azure-ml-py)
  - Discussions

- Afternoon
  - Follow [path 1: AutoML for Many Models](https://github.com/microsoft/solution-accelerator-many-models#using-automated-ml-to-train-the-models) (for both training and inferencing)
  - (Optional) Follow [path 2: Custom ML models for Many Models](https://github.com/microsoft/solution-accelerator-many-models#using-a-custom-training-script-to-train-the-models)
  - Discussions

---

## Agenda: ML/IoT/DevOps Hands on Workshop

### Day 1: Azure ML Basic - full instructions [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/agendas/mlops-edge/Day1-AzureML.md)

- Common
  - 09:30-10:00 Workshop overview, scope, expectations

- ML Track
  - 10:00-10:50 Dev environment setup: Azure ML service Workspace and Azure Notebooks. Authenticate, prepare compute (Azure ML Compute)
  - 11:00-11:50 Train first DL model on Azure Notebooks using Azure ML Compute
  - 13:00-14:50 Distributed training with Horovod on AML Compute, explore AML Workspace
  - 15:00-16:50 Create container images, deploy to Azure Container Instance (and/or Azure Kubernetes Service)
  - 17:00-17:50 Questions and answers

### Day 1 (halfday version): Azure ML Basic - full instructions [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/agendas/mlops-edge/Day1-AzureML-halfday.md)

- Prepare (before workshop)
  - Check Azure subscriptoin
  - Install
  
- Afternoon
  - 14:00-14:50 Workshop overview, scope, expectations and getting started
  - 15:00-15:50 15:00-15:50 Visit AML studio, create computes and try Notebooks
  - 16:00-16:50 16:00-16:50 Try Automated ML
  - 17:00-17:50 17:00-17:50 Check out Designer and MLOps

### Day 2: IoT and Edge Basic

- IoT Track
  - 09:30-10:00 Dev environment setup, Azure Resource creation (IoT Hub, DPS, Cosmos DB, ASA, Storage, etc)
  - 10:00-10:30 Set-up Raspberry Pi
  - 10:40-11:00 Run D2C message application on Pi
  - 11:00-11:50 Provision a device using Azure IoT DPS (X.509 Individual Enrollment)
  - 13:00-13:50 D2C message, Azure Stream Analytics, Data to Storage/DB
  - 14:00-17:50 Custom Vision Edge module deployment

### Day 3: ML + IoT Edge + DevOps - full instructions [here](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/agendas/mlops-edge/Day3-DevOps-ML-IotEdge.md)

- ML+IoT Edge+DevOps Track
  - 09:30-10:00 Day 1, 2 reflection, Day 3 expectations
  - 10:00-11:50 Dev environment setup: Use GitHub Desktop, Azure DevOps(create DevOps account, Organization), create from Azure ML template, customize Build Pipeline
  - 13:00-14:50 Customize Release Pipeline, Git clone using personal token, test CI build
  - 15:00-16:50 Integrate with IoT Edge deployment
  - 17:00-17:50 Questions and answers
