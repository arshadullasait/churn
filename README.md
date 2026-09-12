# Customer Churn Prediction 🚀

This project leverages machine learning to predict customer churn, a critical task for businesses aiming to retain their customers. Businesses can take proactive steps to improve customer satisfaction and reduce churn rates by predicting which customers are likely to leave.

## 🌟 Project Overview

The project uses a logistic regression model to predict customer churn based on various features extracted from a dataset. The model is trained using the data provided in the `WA_Fn-UseC_-Telco-Customer-Churn.csv` file, including tenure, monthly charges, total charges, and various other customer attributes.

### Key Features:
- **End-to-end Pipeline**: The project includes an end-to-end pipeline managed with Apache Airflow, from data extraction and preprocessing to model training and deployment.
- **AWS Integration**: The project leverages AWS services such as S3 and SageMaker to perform model training in a scalable and efficient environment.
- **Dockerized Environment**: The project environment is fully containerized using Docker, ensuring easy setup and consistent performance across different environments.
- **Flask Application**: A Flask web application is included to serve predictions, making the model accessible through a simple web interface.
- **REST API**: The project provides a REST API endpoint for making predictions programmatically, enabling easy integration with other applications.

## 🛠 Pipeline Visualization

<div style="text-align: center;">
  <img src="Pipeline.png" alt="Pipeline" width="80%">
</div>

The pipeline follows a simple yet effective workflow: it starts by downloading the dataset, then moves on to training the model, and finally, a Flask application is deployed to serve predictions. Each task is managed and orchestrated by Apache Airflow, ensuring smooth and automated execution.

## 🔧 Technologies & Tools

- **Python**: The core language used for data processing and model building.
- **Pandas & Scikit-Learn**: Essential libraries for data manipulation and machine learning.
- **Boto3**: AWS SDK for Python, used for interaction with AWS services.
- **Apache Airflow**: Workflow management platform for orchestrating the pipeline.
- **AWS S3 & SageMaker**: Used for storing data and running machine learning jobs in the cloud.
- **Docker**: Containerization of the environment to ensure consistent execution.
- **Flask**: A lightweight web framework for serving predictions.
- **GitHub**: Version control and collaboration platform.

## 📁 Project Structure

```bash
Customer Churn Prediction Project/
├── Dockerfile                       # Docker configuration for setting up the environment
├── airflow/
│   ├── dags/
│   │   └── churn_prediction_dag.py  # Airflow DAG definition
│   └── docker-compose.yaml          # Configuration for running Airflow and other services
├── flask_app/                       # Flask application for serving predictions
│   ├── static/
│   │   └── styles.css               # CSS for the web interface
│   ├── templates/
│   │   └── index.html               # HTML template for the web interface
│   ├── app.py                       # Flask application script
│   ├── Dockerfile                   # Docker configuration for the Flask app
│   └── requirements.txt             # Python dependencies for the Flask app
├── train.py                         # Model training script
├── WA_Fn-UseC_-Telco-Customer-Churn.csv # Dataset
└── README.md                        # Project documentation (you're reading it now!)
               # Project documentation (you're reading it now!)
```
## 🚀 Getting Started

### Prerequisites

Ensure the following are installed on the local machine:

- Docker & Docker Compose
- Git

### Installation
**Clone the repository:**

```bash
git clone https://github.com/arshadullasait/churn.git
cd churn



```
Build and run the Docker containers:
```
docker-compose up -d
```

**Access Apache Airflow:**

Once the containers are up and running, access the Airflow web UI by navigating to http://localhost:8080 in the browser.

**Running the Pipeline**
1. Trigger the DAG: In the Airflow web UI, navigate to the churn_prediction_pipeline DAG and trigger it manually to start the pipeline.

2. Monitor the DAG: Monitor the progress and logs of each task in the pipeline through the Airflow interface.

## 🧠 Training the Model
The model training is handled within the `train_model` task in the Airflow DAG. This task:

* Downloads the dataset from S3.
* Preprocesses the data (handling missing values, encoding categorical variables, etc.).
* Trains a logistic regression model.
* Uploads the trained model back to S3 for future predictions.

## 🌐 Deploying the Flask App
The Flask app is deployed as a Docker container and serves the predictions based on the trained model:

1. Run the Flask App: The app can be run manually using Docker or automatically as part of the Airflow pipeline.
2. Access the Web Interface: Navigate to http://localhost:5000 in the browser to access the prediction interface.

<div style="text-align: center;">
  <img src="UI.png" alt="Pipeline" width="100%">
</div>

## 🌐 Using the REST API

In addition to the web interface, the project also exposes a REST API for making predictions programmatically. This API can be accessed at the following endpoint:

**Endpoint**: `/api/predict`

**Method**: `POST`

**Content-Type**: `application/json`

**Request Body Example**:
```json
{
  "tenure": 12,
  "MonthlyCharges": 70.5,
  "TotalCharges": 800,
  "gender": "Male",
  "SeniorCitizen": "No",
  "Partner": "Yes",
  "Dependents": "No",
  "PhoneService": "Yes",
  "MultipleLines": "No",
  "InternetService": "Fiber optic",
  "OnlineSecurity": "No",
  "OnlineBackup": "Yes",
  "DeviceProtection": "Yes",
  "TechSupport": "No",
  "StreamingTV": "No",
  "StreamingMovies": "No",
  "Contract": "Month-to-month",
  "PaperlessBilling": "Yes",
  "PaymentMethod": "Electronic check"
}
```
**Response Example**:
```
{
  "prediction": 1  // 1 indicates the customer is likely to churn, 0 indicates they are not
}
```

**Accessing the API**:
You can access the API by making a POST request to `http://localhost:5000/api/predict` with the appropriate JSON payload.

## 📊 Results & Evaluation
Once the model is trained, it will be stored in the `model-output/` directory in the specified S3 bucket. The model's performance can be evaluated based on accuracy, precision, recall, and F1-score using standard classification metrics in scikit-learn.

## 💡 Future Work
* Model Improvement: Experiment with other models like Random Forest, Gradient Boosting, or even deep learning models to improve performance.
* Hyperparameter Tuning: Implement hyperparameter tuning using GridSearchCV or RandomizedSearchCV.
