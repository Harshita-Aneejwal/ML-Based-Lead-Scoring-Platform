# ML-Based-Lead-Scoring-Platform

## Topics Covered

* Overview
* Motivation
* Setup
* Technical Aspects
* Demo

---

## Overview

The objective of this project is to predict whether a customer lead is likely to purchase a product or service. The project demonstrates an end-to-end MLOps workflow for lead scoring, including data preprocessing, model training, experiment tracking, and inference automation using **Apache Airflow** and **MLflow**.

**PyCaret**, an open-source AutoML framework, is used for model experimentation and selection. During experimentation, **LightGBM** achieved the best performance for lead conversion prediction. The project also includes unit testing using **PyTest** to ensure the reliability of preprocessing components and data transformation pipelines.

---

## Motivation

This project is based on a case study involving an EdTech startup seeking to optimize its marketing expenditure and reduce Customer Acquisition Cost (CAC).

High CAC can result from:

1. Incorrect targeting
2. High competition
3. Inefficient conversion processes

This project focuses on improving the **Lead-to-Application Completion** metric by identifying high-quality leads that are more likely to convert.

A lead is generated when a visitor shares their contact information on the platform. However, not all leads are genuinely interested in the offered service. These low-intent or junk leads create inefficiencies in the sales pipeline and consume valuable resources.

The goal of this platform is to classify leads based on their likelihood of conversion, enabling sales teams to prioritize promising prospects and improve operational efficiency.

---

## Technical Aspects

### Project Pipelines

The platform consists of three major pipelines:

#### 1. Data Pipeline

Processes and transforms raw lead data into a structured format suitable for machine learning.

#### 2. Training Pipeline

Performs preprocessing, feature engineering, model training, and model registration.

#### 3. Inference Pipeline

Applies preprocessing and generates predictions for new incoming leads.

---

### Exploratory Data Analysis (EDA) & Preprocessing

The dataset primarily contains features describing:

* Lead acquisition sources
* Marketing channels
* Website interaction behavior
* User engagement metrics

EDA was performed using **Pandas Profiling**.

#### Key EDA Observations

* Large number of missing values across several features
* Only a few categories contribute significantly to:

  * `first_platform_c`
  * `first_utm_source_c`
  * `first_utm_medium_c`
* Several interaction features contain more than 99% missing values

#### Data Preprocessing Steps

* Reduced high cardinality in the `city_mapped` feature by grouping cities into Tier-1, Tier-2, and Tier-3 categories.
* Consolidated low-frequency categories in marketing source features into an `Others` category using cumulative frequency thresholds.
* Replaced null values in:

  * `total_leads_dropped`
  * `referred_leads`
* Categorized 37 interaction-related features into:

  * Assistance Interaction
  * Career Interaction
  * Payment Interaction
  * Syllabus Interaction

Data preprocessing notebook:

https://github.com/Harshita-Aneejwal/ML-Based-Lead-Scoring-Platform/blob/master/Lead_scoring_data_pipeline/data_cleaning_template.ipynb

---

### Model Experimentation

**PyCaret** was used to automate model experimentation, evaluation, and comparison.

The experimentation process included:

* Automated preprocessing
* Feature selection
* Model comparison
* Hyperparameter optimization
* MLflow experiment tracking

After removing irrelevant features identified during initial experiments, model performance improved significantly.

The best-performing model was **LightGBM**, which was selected based on prediction accuracy.

Model experimentation notebook:

https://github.com/Harshita-Aneejwal/ML-Based-Lead-Scoring-Platform/blob/master/notebooks/lead_scoring_model_experimentation.ipynb

---

### Experiment Tracking with MLflow

MLflow is used to:

* Track experiments
* Compare model runs
* Store model artifacts
* Register trained models
* Maintain reproducibility

PyCaret automatically logs experiments to MLflow using the configured tracking server.

---

### Unit Testing

The project includes PyTest-based unit tests covering key preprocessing functionalities:

1. Testing data loading operations
2. Verifying city-tier mapping logic
3. Validating categorical feature mappings
4. Testing interaction category mappings

Test cases:

https://github.com/Harshita-Aneejwal/ML-Based-Lead-Scoring-Platform/tree/master/unit_test

---

## Technology Stack

* Python
* Apache Airflow
* MLflow
* PyCaret
* LightGBM
* Pandas
* NumPy
* Scikit-learn
* PyTest
* SQLite
* Jupyter Notebook

---

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Harshita-Aneejwal/ML-Based-Lead-Scoring-Platform.git
cd ML-Based-Lead-Scoring-Platform
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Install Apache Airflow

Follow the official Airflow installation guide for your operating system.

### 4. Configure Airflow

Create an Airflow admin user:

```bash
airflow users create \
    --username admin \
    --firstname Harshita \
    --lastname Aneejwal \
    --role Admin \
    --email harshita@example.com \
    --password your_password
```

Start the Airflow web server:

```bash
airflow webserver -p 8080
```

Start the Airflow scheduler:

```bash
airflow scheduler
```

---

### 5. Configure MLflow

Start the MLflow tracking server:

```bash
mlflow server \
--backend-store-uri sqlite:///mlflow.db \
--host 0.0.0.0 \
--port 5000
```

---

## Project Structure

```text
ML-Based-Lead-Scoring-Platform/
│
├── Lead_scoring_data_pipeline/
├── notebooks/
├── unit_test/
├── dags/
├── data/
├── models/
├── requirements.txt
└── README.md
```

---

## Demo

Screenshots and workflow demonstrations can be found in:

https://github.com/Harshita-Aneejwal/ML-Based-Lead-Scoring-Platform/blob/master/MLOPS.pdf

---

## Business Impact

This platform helps organizations:

* Improve lead qualification accuracy
* Reduce customer acquisition costs
* Prioritize high-conversion prospects
* Improve sales team productivity
* Automate machine learning workflows
* Maintain reproducible ML experiments

---

## Future Improvements

* Real-time lead scoring API deployment
* Model monitoring and drift detection
* Automated retraining pipelines
* Cloud deployment on AWS
* Dashboard for lead analytics and visualization
* CI/CD integration for MLOps workflows

---

## License

This project is intended for educational and learning purposes.
