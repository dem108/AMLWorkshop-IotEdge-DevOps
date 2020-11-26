# Day 1: Automated ML and ML Pipeline basics

- Pre-requisites for Day 1
  - Python skills
  - Understanding of [key concepts of Azure ML](https://docs.microsoft.com/en-us/azure/machine-learning/concept-azure-machine-learning-architecture)
  - Get familiar with Azure ML by running other experiments, trying own datasets, extending from previous workshops
  - Bring any questions on overall Azure ML, share your feedbacks so far before Day 1

- Day 1 morning
  - Intro to agenda, getting to know each other
  - Fundamentals
    - Creating [dev environment](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-environment): Azure ML Workspace, Compute Instance, Compute Clusters
    - [What happens when a job is submitted](https://docs.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model#understand-what-happens-when-you-submit-a-training-job)
    - Managing experiments and [models](https://docs.microsoft.com/en-us/azure/machine-learning/concept-model-management-and-deployment)
    - Automated ML: [key concept](https://docs.microsoft.com/en-us/azure/machine-learning/concept-automated-ml)
    - Deployment: [process](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-and-where?tabs=azcli) recap and [init/run](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-and-where?tabs=azcli#define-an-entry-script) structure
    - (Optional) Monitoring ([swagger](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-advanced-entry-script#automatically-generate-a-swagger-schema) and [app insights](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-app-insights))
    - (Optional) Light touch on others ([pipeline](https://docs.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines), [designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines#building-pipelines-with-the-designer), [data drift](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets), [interpretability](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-machine-learning-interpretability) etc)
  - Discussions

- Day 1 afternoon
  - Automated ML
    - Recap [options](https://docs.microsoft.com/en-us/azure/machine-learning/concept-automated-ml)
    - [Things covered by Automated ML, things covered by people](https://docs.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls)
    - How to check [logs & outputs](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-save-write-experiment-files)
  - ML Pipeline
    - [Getting started sample](https://aka.ms/pl-get-started)
    - [Data dependency sample](https://aka.ms/pl-data-dep)
    - [AutoMLStep sample](https://aka.ms/pl-automl)
    - [Quick intro to ParallelRunStep](https://github.com/Azure/MachineLearningNotebooks/tree/master/how-to-use-azureml/machine-learning-pipelines/parallel-run)
  - Discussions
