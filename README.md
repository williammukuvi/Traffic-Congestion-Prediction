# Traffic-Congestion-Prediction
A machine learning project predicting traffic congestion using Azure ML and the Metro Interstate Traffic Volume dataset
# Traffic Congestion Prediction Model

This project leverages Azure Machine Learning's Automated ML to predict traffic congestion based on weather and time-related features. The dataset used is the **Metro Interstate Traffic Volume** dataset, and the model predicts the volume of vehicles based on features like temperature, cloudiness, and time of day.

## Project Features
- **Dataset**: Metro Interstate Traffic Volume (from Kaggle)
- **Tech Stack**: Azure Machine Learning, Python, JSON
- **Model Type**: Regression model predicting traffic volume
- **Input Structure**: JSON input with features like holiday, weather, and date-time
- **Output**: Predicted traffic volume in real-time or batch processing

## Files
- `MLTable.yaml`: MLTable definition for Azure ML dataset.
- `traffic_prediction.json`: Sample JSON input for traffic predictions.
