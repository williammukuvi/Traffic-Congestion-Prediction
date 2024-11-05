# Traffic Congestion Prediction Model

This repository contains a predictive model for forecasting traffic congestion levels, developed using **Microsoft Azure Machine Learning**. Leveraging the Metro Interstate Traffic Volume dataset, this model predicts traffic volume based on time and weather data, enabling real-time predictions through a web service endpoint.

## Project Overview

In this project, we utilized **Azure Machine Learning’s Automated ML** to train and deploy a model for predicting traffic volume. By using a dataset that includes historical traffic volume along with weather and time features, the model provides valuable predictions to aid in traffic management.

### Key Features

- **Automated ML**: Automatically selected the best regression model and optimized parameters for traffic volume prediction.
- **Real-Time Predictions**: Endpoint deployed for on-demand predictions, using JSON inputs with time and weather-based features.
- **Weather and Time Analysis**: Leverages features such as temperature, cloud cover, and hour of day to accurately predict traffic congestion.

## Dataset

**Metro Interstate Traffic Volume dataset**

- Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Metro+Interstate+Traffic+Volume)
- Description: Contains hourly traffic volume data with associated weather and time information, providing features for accurate traffic prediction.

## Getting Started

### Prerequisites

- **Microsoft Azure account**: Access to Azure Machine Learning services.
- **Azure Machine Learning SDK for Python**: Install using `pip install azureml-sdk`.
- **Python 3.7+** with required packages (listed in `requirements.txt`).

### 1. Set Up an Azure Machine Learning Workspace
1. Sign in to the [Azure portal](https://portal.azure.com) and navigate to **+ Create a resource**.
2. Search for **Machine Learning** and create a new Azure Machine Learning workspace with the following settings:
   - **Subscription**: Your Azure subscription.
   - **Resource group**: Create or select an existing resource group.
   - **Workspace name**: A unique name for your workspace.
   - **Region**: Closest region to you.
   - **Storage account**: Note the default storage account created.
   - **Key vault**: Note the default key vault.
   - **Application insights**: Default insights created for the workspace.
3. Select **Review + create**, then **Create**. After deployment, go to the resource and select **Launch studio** or open [Azure Machine Learning studio](https://ml.azure.com).

### 2. Create and Register the Dataset
1. Download the Metro Interstate Traffic Volume dataset.
2. In Azure Machine Learning studio, under **Datasets**, select **+ Create dataset** > **From local files**.
3. Provide the following dataset settings:
   - **Name**: `traffic-volume`
   - **Description**: Historical traffic volume data with weather and time features.
   - **Type**: Table (`mltable`)
4. Select **workspaceblobstore** as the destination storage, upload the dataset, and create the dataset.

### 3. Train the Model with Automated ML
1. In Azure Machine Learning studio, under **Automated ML**, select **+ New automated ML job**.
2. Configure the job settings:
   - **Job name**: Auto-generated or custom.
   - **Experiment name**: `traffic-congestion-prediction`
   - **Description**: Automated ML for traffic volume prediction.
3. Set the **Task type** to **Regression**, select the `traffic-volume` dataset, and specify the **Target column** as the field representing traffic volume.
4. Additional configuration:
   - **Primary metric**: Select `NormalizedRootMeanSquaredError`.
   - **Enable early termination**: Enable to reduce training time.
   - **Allowed models**: Choose RandomForest and LightGBM for faster training (you can expand as needed).
   - **Limits**: Set max trials to 3, concurrent trials to 3, and experiment timeout to 20 minutes.
5. Select the compute target (e.g., a **Standard_DS3_v2** virtual machine) and submit the job.

### 4. Review and Select the Best Model
1. Once the job is complete, view the **Overview** tab to see the best model summary.
2. Note the selected algorithm, and review metrics such as residuals and predicted vs. true charts.
3. Select the best-performing model based on its primary metric score.

### 5. Deploy the Model
1. On the **Model** tab of the best model, select **Deploy** and choose **Real-time endpoint**.
2. Configure the deployment:
   - **Virtual machine**: Standard_DS3_v2
   - **Instance count**: 3 (adjust as necessary)
   - **Endpoint**: Create a new endpoint or use the default.
3. Wait for the model to deploy. Once deployment is complete, navigate to the **Endpoints** tab to view and test the deployed model.

### 6. Test the Deployed Endpoint
1. In Azure Machine Learning studio, under **Endpoints**, open the deployed endpoint.
2. In the **Test** tab, enter sample JSON input data:
   ```json
   {
     "data": [
       {
         "temp": 293.15,
         "rain_1h": 0.0,
         "clouds_all": 20,
         "weather_main": "Clear",
         "hour": 17,
         "day_of_week": 4
       }
     ]
   }
