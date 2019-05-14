# AMLWorkshop-IotEdge-DevOps
> ML/IoT/DevOps Hands on workshop

## Agenda
### Day 3 / 2019년 5월 17일(금)

#### ML+IoT Edge+DevOps Track
- **09:30-10:00 Day 1, 2 reflection, Day 3 expectations**
    1. Reflect what we've learn in Day 1 and Day 2

    1. Check out basic concept: [MLOps](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-model-management-and-deployment)

    1. Also check out this [MLADS tutorial](https://github.com/dem108/AMLWorkshop-IotEdge-DevOps/blob/master/doc/decks/219_Tutorial_MLADS_DevOps_for_AI_Praneet_Dmitry.pdf)

    1. There's a great guideline [LearnAI_Azure_ML](https://github.com/Azure/LearnAI_Azure_ML/tree/master/devops) (a GitHub repo), but we will leave this as further exercise for you. 

    1. Note the coverage for today:
        - We'll use template to start quickly, instead of developing DevOps pipeline from scratch.
        - We'll make it work, test CI/CD, then tweak a bit to use IoT Edge for deployment target.
        - At the end of the day, initiate the CI/CD pipeline with `git commit`, and track the pipeline run. 

- **10:00-11:50 Dev environment setup: Use GitHub Desktop, Azure DevOps(create DevOps account, Organization), create from Azure ML template, customize Build Pipeline**

    1. Create an Azure DevOps account from [DevOps start page](https://azure.microsoft.com/en-us/services/devops/?nav=min) - `Start Free`
        What you also create is an `organization`. Note the organization name created.

    1. We will use this quick starter - [Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/?name=azure%20machine%20learning)
    
        1. Alternative way to do this is [LearnAI_Azure_ML](https://github.com/Azure/LearnAI_Azure_ML/tree/master/devops), which helps you with step-by-step approach to create the pipeline from scratch. We will ***not*** use this in this workshop.

    1. From the Demo Generator, choose the template, `Azure Machine Learning`. It's under `DevOps Labs` tab. Choose your `organization`, and specify the project name to create. 
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-generator-01-create-with-azureml-template.jpg)
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-generator-02-create-with-azureml-template.jpg)

    1. Explore Repos
        1. Edit config.json under aml_config. You can obtain the content for this file from AML service Workspace `Overview` from Azure Portal.
        1. Notice that editing this file lets to commit it to master branch, which will initiate the Build Pipeline. It will fail and we'll fix the issue in the following steps.
            - You can alternatively commit it to another branch, and merge it later into the master branch. A general git practice.

        > Note: Instead of keeping sensitive files in Repo you could use `Secure File` feature from Azure Pipelines. A sample guidance is [here](https://github.com/Azure/LearnAI_Azure_ML/blob/master/devops/01-Build.ipynb). More details on Secure Files [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/secure-files?view=azure-devops).
    1. Explore Pipelines
    1. Edit Build Pipeline `DevOps-for-AI-CI`
        1. Starting from `Create or Get Workspace`, specify the Azure subscription to use, and authorize.
        1. Save and Queue.
        1. Monitor the run, and fix any outstanding issues.

        > Note: We are using Azure CLI Authentication now. Check out other ways to [authenticate](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/manage-azureml-service/authentication-in-azureml/authentication-in-azure-ml.ipynb).

- **13:00-14:50 Customize Release Pipeline, Git clone using personal token, test CI build**

    1. Open `Deploy Webservice` Release Pipeline. Notice that releases were automatically initiated but failed.
    
    1. Click `Edit` for the Release Pipeline. Check out `Pre-deployment conditions`, and `Post-deployment conditions` for each stage.

        1. In the `Prod - Deploy on AKS` stage, check out `Gates`. See what deployment gates can be added.

        1. Click `1 job, 4 tasks` under `QA - Deploy on ACI` stage.

        1. Specify Azure subscriptions to use for deployment and test.

        1. Continue to the `Prod - Deploy on AKS` stage and do the same.

    1. The release pipeline is ready. Now let's clone the repo locally, and try committing it to initiate the whole process.

        1. Create a `Personal access credential` from Azure DevOps portal. To do that:
            1. Click your account icon from top right. Click `Security`. Click `Personal access tokens` from left pane.
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-git-clone-your-repo-create-personal-token1.jpg)

            1. Click `New token`. Specify scope for this token. In this workshop, allow read and write for Code.
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-git-clone-your-repo-create-personal-token2.jpg)

            1. When you click `Create`, a token is created. Copy this to somewhere.
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-git-clone-your-repo-create-personal-token3.jpg)

        1. Click Repos from Azure DevOps. Copy the URL of your repo. It looks like this:
            `https://dev.azure.com/<org name>/<project name>/_git/<repo name>`

        1. Git clone using GitHub Desktop. To do that:
            1. From the local computer, open GitHub Desktop.
            1. Open File menu, click `Clone repository`.
            1. Click URL tab, paste the URL copied above.
            1. Make sure the local path does not contain any files.
            1. It will ask you to authenticate. Use your Azure account and personal access token you created above.
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-git-clone-your-repo-with-personal-token.jpg)

        1. Use VS Code or any other editor to open the local repo.
        
        1. Let's edit AKS cluster definition to use Standard_D3_V2 instead of Standard_F2 (unless you have already increased quota in your region). To do that:

            1. Open `51-deployOnAks.py`, click `Edit`, and change the `vm_size` parameter of `AksCompute.provisioning_configuration()` to `Standard_D3_v2` (be careful - case sensitive).

                ```python
                except:
                    aks_name = "aks" + datetime.datetime.now().strftime("%m%d%H")
                    aks_service_name = "akswebservice" + datetime.datetime.now().strftime("%m%d%H")
                    prov_config = AksCompute.provisioning_configuration(
                        agent_count=6, vm_size="Standard_D3_v2", location="eastus"
                    )
                    print(
                        "No AKS found in aks_webservice.json. Creating new Aks: {} and AKS Webservice: {}".format(
                            aks_name, aks_service_name
                        )
                    )
                ```
        
        1. Git commit and git push (using command line or GitHub Desktop). Monitor Pipeline initiation.
            1. If needed, delete existing Image and/or Model from Azure ML service Workspace before testing.
            1. If the first stage (`QA - Deploy on ACI`) in the Release Pipeline was succesful, it will wait for your Approval for the second stage (`Prod - Deploy on AKS`)
            1. Approve and monitor the final stage.
                Note: Current `61-AksWebserviceTest.py` deletes the web service (deployment) at the end. Change if needed.

        1. If you want to re-test CI/CD, you may make any arbitrary change (for example README.md), and do git commit and git push. 

- **15:00-16:50 Integrate with IoT Edge deployment**

    1. We'll create a DevOps Project from Azure Portal this time, leveraging [this](https://docs.microsoft.com/ko-kr/azure/iot-edge/how-to-devops-project) and [this](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-ci-cd), and an additional sample code (shared below). 
    
    1. Create new `DevOps Project`.
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-01-new-project.jpg)
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-02-python.jpg)
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-Io`tEdge-DevOps/master/doc/images/devops-iot-03-simple-iotjpg.jpg)
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-04-name-project-iothub.jpg)

        - IoT Hub is also created.

    1. You can now go to dev.azure.com and continue browsing.
    
    1. First disable CI for a moment. To do that:
        1. Go to Pipelines - Build Pipelines.
        1. Click `Triggers` tab, uncheck `Enable continuous integration`, save.

    1. Git clone its repo. Create a personal token if needed.

    1. Copy [these files(TBD)]()(`VisionSampleModule`) into `/modules/VisionSampleModule` of that local repo, git commit, and git push. Now the additional module for our Edge deployment is added.
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-05-sample-module-added.jpg)

    1. Rename `/deployment.template.json` into `/deployment.template.basic.json`

    1. Copy [this file(TBD)]() to `/` as `/deployment.template.visionsample.json` of local repo.

    1. Then git commit and git push.
        ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-06-uploaded-files.jpg)

    1. Modify Build Pipelines to work on our `VisionSampleModule`, not the original sample. To do that:
        1. Go to Build Pipeline, edit the Build Pipeline.
            - deployment template: `deployment.template.visionsample.json`
            - platform: `arm32v7`
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-07-update-build-pipeline.jpg)

        1. Click `Variable` tab, add variable `REGISTRYNAME`
            ![](https://raw.githubusercontent.com/dem108/AMLWorkshop-IotEdge-DevOps/master/doc/images/devops-iot-08-update-build-pipeline-variable.jpg)

        1. `Save` and `Queue` to test the build.

    1. Go to Azure Portal, open the IotHub created above, choose `IoT Edge` from left pane. Click the edge device `myEdgeDevice`, copy connection string and register it on AI Camera.

    1. Test locally.

    1. Enable CI. To do that:
        1. Go to Pipelines - Build Pipelines.
        1. Click `Triggers` tab, check `Enable continuous integration`, save.

    1. Test with git commit.
    

- **17:00-17:50 Questions and answers**


