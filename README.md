*NOTE:* This file is a template that you can use to create the README for ymy project. The *TODO* comments below will highlight the information you should be sure to include.


# Operationalizing-Machine-Learning

## Overview
This project is part of the Udacity Azure ML Nanodegree (Microsoft Azure Machine Learning Engineer with Microsoft Azure - Course 3: ). In this project, I use the Bank marketing datasets and Azure to configure a cloud-based machine learning production model, deploy it, and consume it. I also created, published, and consumed a pipeline to automate the process.

## Architectural Diagram
Here is my architecture diagram for this project:

**Deploy the Model - Running Jupyter Notebook file: deploy-model-inazure-ML.ipynb**
![alt text](<screenshots/Project 2 - Architechture diagram.PNG>)

**Publish Pipeline - Running Jupyter Notebook file: public-an-machine-learning-pipeline.ipynb**

![alt text](<screenshots/Project 2 - Architechture diagram - pipeline.PNG>)

Let me explore some key of the component in this project:
- **1. Authentication**: In this step, I need to create a Security Principal (SP) to interact with the Azure Workspace. Since I used the Udacity lab for the project, I skipped this step
- **2. Automated ML Experiment**: In this step, I create an experiment using Automated ML, configure a compute cluster, and use that cluster to run the experiment.
- **3. Deploy the best model**: Deploying the Best Model will allow us to interact with the HTTP API service and interact with the model by sending data over POST requests.
- **4. Enable logging**: Logging helps monitor my deployed model. It helps us know the number of requests it gets, the time each request takes, etc.
- **5. Swagger Documentation**: In this step, I consume the deployed model using Swagger.
- **6. Consume model endpoints**: I interact with the endpoint using some test data to get inference.
- **7. Create and publish a pipeline**: In this step, I automate this workflow by creating a pipeline with the Python SDK.

## Key Steps
**1. Authentication**

I used the lab Udacity for this exercise, so I skipped this step since I'm not authorized to create a security principal.

**2. Automated ML Experiment**

For this step, I used the **deploy-model-inazure-ML.ipynb** Jupyter Notebook file to create a Automated ML Experiment.
I created an AutoML experiment to run using the **Bank Marketing Dataset** loaded in the Azure Workspace, choosing 'y' as the target column.
I uploaded this dataset into Azure ML Studio in the Registered Dataset Section using the Local file or URL provided in the project.
I used the **Standard_DS3_v2** for the Virtual Machine and 1 as the minimum number of nodes.
I ran the experiment using classification, without enabling Deep Learning. The run took some time to test various models and find the best model for the task.
From my run, the best-performing model is the voting ensemble as shown below.

**Registered Dataset**
![alt text](<screenshots/1. Registered Dataset.png>)

**Created Compute Instance**
![alt text](<screenshots/2. Compute instances.png>)

**Created Compute Cluster**
![alt text](<screenshots/3. Compute cluste.png>)

**Experiment Created**
![alt text](<screenshots/4. Experiment.png>)

**Created AutoML Experiment**
![alt text](<screenshots/3. Created AutoML Exprements.png>)

**running AutoML Experiment**
![alt text](<screenshots/4. run Auto ML Experiment.png>)

**Best Model**

****List of the Best models****
![alt text](<screenshots/6. List of Best models (Algorithm name).png>)

****the Best models****
![alt text](<screenshots/7.  The best model.png>)

****Best model metrics****
![alt text](<screenshots/7.1. the Best model with Metric (1).png>)
![alt text](<screenshots/7.1. the Best model with Metric (2).png>)

**3. Deploy Best Model**

The best model from my AutoML run is deployed into production using Azure Container Instance (ACI) and I can access endpoints through which other services can interact with my deployed model. 
I also enable authentication during deployment so keys are generated that other services can use to authenticate before interacting with my deployed model.

**Deploy the best model using Azure Container Instance (ACI) with Authentication enabled**
![alt text](<screenshots/8. Deploy Model.png>)

**4. Enable logging**

After deploying the best model, I can enable Application Insights and retrieve logs.
Enabling Application Insights and Logs could have been done at the time of deployment, but for this project, I achieved it using Azure Python SDK. Running the **logs.py** script requires interactive authentication
![alt text](<screenshots/azure login.PNG>)

I enable application insights by adding this line to the script: **service.update(enable_app_insights = True)**
![alt text](<screenshots/update the endpoints script.PNG>)

Running **logs.py** file
![alt text](<screenshots/logs.py - 1.PNG>)
![alt text](<screenshots/logs.py - 2.PNG>)

Application Insights Enable change status from False to True
![alt text](<screenshots/10. Application Insights enabled.png>)

Deploy Endpoints success with REST endpoint, Swagger URL
![alt text](<screenshots/Enable insignt.PNG>)

![alt text](<screenshots/pubplished pipeline.PNG>)

**5. Swagger Documentation**

To consume my best AutoML model using Swagger, I first need to download the **swagger.json** file provided to us in the Endpoints section of Azure Machine Learning Studio. Then I run the **swagger.sh** and **serve.py** files to be able to interact with the swagger instance running with the documentation for the HTTP API of the model.

Update info in swagger.sh file
![alt text](<screenshots/swagger sh.PNG>)

**Running Swagger in docker**
![alt text](<screenshots/run docket and swagger .png>)
[text](<screenshots/swagger sh.png>)
**Localhost**
![alt text](<screenshots/Run localhost for swagger (1).png>)
![alt text](<screenshots/localhost running.png>)

**Swagger documentation for the HTTP API of the model**
![alt text](<screenshots/swager localhost 9000.PNG>)
![alt text](<screenshots/swagger - localhost 8000.PNG>)
![alt text](<screenshots/swagger - explore 2.PNG>)
![alt text](<screenshots/swagger - explore 3.PNG>)
![alt text](<screenshots/swagger - explore 4.PNG>)

**6. Consume model Endpoints**
In order to interact with the model and feed some test data to it, i add **the scoring_uri and  the key** to the **endpoint.py** script and run it.

Shows the REST Endpoint link with primary key and secondary keys.
![alt text](<screenshots/Rest Endpoint and Key.PNG>)

Use the scoring URL and the primary key to update the **endpoints.py** script.
![alt text](<screenshots/update the endpoints script.PNG>)

Execute the **Endpoint.py** script to get the inference from the deployed model
![alt text](screenshots/endpoints.PNG)

Run **Endpoint.py**, A data,json file appear
![alt text](<screenshots/data json is produced.PNG>)

**7. Create and publish a pipeline**

For this step, I used the **public-an-machine-learning-pipeline.ipynb** Jupyter Notebook file to create a Pipeline. I created, consumed and published the best model for the bank marketing dataset using AutoML with Python SDK.

**Create a Pipeline in the SDK**
![alt text](<screenshots/11. create pipeline.png>)

**Pipeline in Azure Studio**
![alt text](<screenshots/12. pipeline running.png>)

**Pipeline training**
![alt text](<screenshots/12. pipeline running (2).png>)

**Run Completed**
![alt text](<screenshots/12. pipeline training completed.png>)

**Run Completed - Metric outputs**
![alt text](<screenshots/13. pipeline best models.png>)
![alt text](<screenshots/14. pipeline the best model (metric - 1).png>)
![alt text](<screenshots/14. pipeline the best model (metric - 2).png>)

**Run Completed - The best model**
![alt text](<screenshots/14. pipeline the best model.png>)

**Consume a pipeline Endpoint - Completed**
![alt text](<screenshots/pipeline with endpoint.png>)

**Pipeline Rest Endpoint - Metrics**
![alt text](<screenshots/the best model pipeline endpoint.png>)

**Created the Pipeline endpoints**
![alt text](<screenshots/Create REST Endpoint - Pipeline endpoint.PNG>)

**Published pipeline overview with status of ACTIVE**
![alt text](<screenshots/pubplished pipeline.PNG>)

**Published pipeline overview with status of Success**
![alt text](<screenshots/published pipeline overview success.PNG>)

**showing the "RunDetails Widget**
Injupiter Notebook, showing the RunDetailsWidget" show the step runs --> at the moment the API no longer to support!
![alt text](<screenshots/RunDetail no longer to supporter.PNG>)

## Screen Recording
- Link to screen recording submission: https://www.veed.io/view/f6979c89-21cd-4d4d-9def-ba981f4c6033?panel=share
- Link to screen recording submission (Youtube): https://youtu.be/mTyj3Bd1PaI

## Standout Suggestions

- Since the data is highly imbalanced, use a technique to first handle the imbalance issue to improve the model predictions
- Enable deep learning which will train more models and may yield a better performing model
- Run on an environment with a stronger CPU/GPU for faster model training
