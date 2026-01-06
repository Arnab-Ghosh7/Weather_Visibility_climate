# Weather Visibility Prediction

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)

> A robust Machine Learning solution for predicting visibility distance based on climatic conditions, featuring automated data validation, clustering-based model selection, and a Flask API.

## 📌 Project Overview
Visibility distance defines the transparency of the atmosphere and is estimated by a human observer or an automated system. It is a critical metric for:
*   **Aviation**: Determining takeoff and landing feasibility.
*   **Transportation**: Ensuring safety on roads and maritime routes during adverse weather.
*   **Logistics**: Planning routes to avoid delays caused by fog, haze, or heavy precipitation.

This project addresses the challenge of predicting visibility by training sophisticated Machine Learning models on historical weather data. Unlike simple regression approaches, this solution acknowledges that weather patterns are highly localized and diverse. To handle this complexity, we implement a **Cluster-Then-Predict** architecture:

1.  **Data Ingestion & Validation**: Raw data is rigorously checked for schema conformity, missing values, and anomalies.
2.  **Clustering (Unsupervised Learning)**: We use **K-Means Clustering** to group data points into distinct "weather regimes" (clusters). Each cluster represents a specific type of weather pattern (e.g., "High Humidity & Low Temp" vs. "Low Humidity & High Pressure").
3.  **Specialized Modeling (Supervised Learning)**: Instead of a generic model for the whole dataset, a specific model is trained for **each cluster**. The system iterates through different algorithms (e.g., Random Forest, XGBoost, Decision Tree) and dynamically selects the best performer for that specific cluster.

This targeted approach significantly improves prediction accuracy by allowing models to specialize in specific weather conditions.

## 🚀 Features
*   **Automated Data Validation**: Checks for filename patterns, column length, and missing values before processing.
*   **Advanced Preprocessing**: Handles missing values (KNN Imputation) and separate features/labels.
*   **Clustering Approach**: Uses `KMeans` (with Elbow Plot validation) to handle data variance by creating separate models for distinct data clusters.
*   **Dynamic Model Tuning**: Automatically tunes hyperparameters using `GridSearchCV` and selects the best model (`XGBRegressor` vs `DecisionTreeRegressor`) for each cluster.
*   **Flask API**: Exposes endpoints for both Training and Prediction triggers.
*   **Monitoring**: Integrated with `Flask-MonitoringDashboard` for performance tracking.
*   **Logging**: Comprehensive logging for all operations (Validation, Training, Prediction).

## 🛠️ Tech Stack
*   **Language**: Python 3.7+
*   **Framework**: Flask
*   **Machine Learning**: Scikit-Learn, XGBoost
*   **Data Manipulation**: Pandas, NumPy
*   **Database**: SQLite (for Dashboard monitoring)

## 📂 Project Structure
```
.
├── application_logging/      # Custom logging modules
├── best_model_finder/        # Logic for hyperparameter tuning and model selection
├── data_ingestion/           # Data loading logic
├── data_preprocessing/       # Preprocessing and Clustering logic
├── DeepL_Folder/             # (Optional) Deep Learning related files
├── file_operations/          # File handling and model saving/loading
├── models/                   # Directory where trained models are saved
├── Prediction_Raw_Data_Validation/ # Validation logic for prediction files
├── training_Validation_Insertion/  # Validation logic for training files
├── main.py                   # Flask Application entry point
├── trainingModel.py          # Training pipeline orchestration
├── predictFromModel.py       # Prediction pipeline orchestration
├── requirements.txt          # Project dependencies
└── README.md                 # Project Documentation
```

## ⚙️ Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/Arnab-Ghosh7/Weather-Visibility-Climate.git
    cd Weather-Visibility-Climate
    ```

2.  **Install Dependencies**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Run the Application**
    ```bash
    python main.py
    ```
    The server will start on `http://localhost:5000`.

## 📡 API Usage

### 1. Train Model
*   **Endpoint**: `/train`
*   **Method**: `POST`
*   **Body**:
    ```json
    {
      "folderPath": "absolute/path/to/training/batch/files"
    }
    ```
*   **Description**: Triggers the training pipeline. Validates data, clusters it, and trains a model for each cluster.

### 2. Predict
*   **Endpoint**: `/predict`
*   **Method**: `POST`
*   **Body**:
    ```json
    {
      "folderPath": "absolute/path/to/prediction/batch/files"
    }
    ```
*   **Description**: Generates predictions for the files in the specified folder using the best-trained models.

## 📊 Deployment
The application includes `Procfile` and `manifest.yml`, making it ready for deployment on platforms like **Heroku** or **Pivotal Cloud Foundry (PCF)**.

## 📝 License
This project is licensed under the MIT License.
