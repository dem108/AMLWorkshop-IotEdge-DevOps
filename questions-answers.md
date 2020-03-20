#### Questions and Answers

- Want to use Custom Docker Image as a base when training a ML model
    - Baseline
        - https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.dnn.tensorflow?view=azure-ml-py
    - What are the base images we can use to create our own custom docker image?
        - Need base image with AML SDK installed
        - Will pull this base image, **install custom libraries manually without using pip or conda** (directly from within the container run using bash)
        - Will push the prepared image to ACR, and use this with ScriptRun from Azure ML
    - Available images (subject to change)
        - `IntelMPI CPU`: `base:intelmpi2018.3-ubuntu16.04`, `base:latest`
        - `OpenMPI CPU` : `base:openmpi3.1.2-ubuntu16.04`
        - `IntelMPI GPU - cuda9`: `base-gpu:intelmpi2018.3-cuda9.0-cudnn7-ubuntu16.04`, `base-gpu:latest`
        - `OpenMPI GPU - cuda9`: `base-gpu:openmpi3.1.2-cuda9.0-cudnn7-ubuntu16.04`
        - `IntelMPI GPU - cuda10`: `base-gpu:intelmpi2018.3-cuda10.0-cudnn7-ubuntu16.04`
        - `OpenMPI GPU - cuda10`: `base-gpu:openmpi3.1.2-cuda10.0-cudnn7-ubuntu16.04`

- HyperDrive는 순수 random인지, 기존에 실행된 결과에 따라 다음 sample이 영향을 받는지

- ML 배포용 AKS에 GPU를 쓸 수 있는지

- 설명에 의하면 Training할 때 생성되는 Container 이미지도 ACR에 등록되고 subsequent runs를 위해 cache된다고 하는데, 이 cache purge는 experiment completion 때 되는지? 실제 학습했던 경우에도 image push가 안되는 것으로 보임.
    - ACR에는 없는데
    - Remote Compute (예 AML Compute)에 존재할 것으로 보임
        - AML Compute 경우면 worker node 다 만들고 나서 Preparing 단계에서 docker pull할 것으로 보임
        - worker node가 삭제되지 않고 남아있는 상태에서 재실행하면 재활용할 것 같음

AML service Workspace: East US

default data store: East US
AML compute: East US
AKS as compute: Korea Central

Supported operation:
- Submit experiment: AKS in Korea Central

Question?
1. Additional Datastore: Korea Central
2. AML Compute: Korea Central

This enables using both datastore and compute from Korea Central, supporting data sovereignty, while using AML service Workspace in other regions

