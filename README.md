# End-to-End MLOps Project: Student Performance Indicator


This project demonstrates a complete end-to-end MLOps pipeline for predicting student performance in mathematics based on various social and academic factors. The entire workflow, from data ingestion and model training to deployment as a web application, is automated and production-ready.



##  workflow

The MLOps pipeline is structured to be modular, scalable, and automated.

1.  **Data Ingestion**: Raw data is ingested from a source (e.g., CSV file, database) and stored in an artifact store.
2.  **Data Validation**: The ingested data is validated against a schema to ensure its quality and integrity.
3.  **Data Transformation**: The validated data is preprocessed. This includes handling categorical features, scaling numerical features, and splitting the data into training and testing sets.
4.  **Model Training**: Several regression models are trained on the preprocessed data. The best model is selected based on performance metrics (e.g., R-squared score).
5.  **Model Evaluation**: The best model is evaluated on the test set to ensure it generalizes well to unseen data.
6.  **Model Deployment**: The trained model, along with the data transformation pipeline, is saved as a pickle file. A Flask API is built to serve predictions.
7.  **CI/CD Automation**: The entire pipeline is automated using GitHub Actions. On every push to the `main` branch, the pipeline runs, a Docker image is built, and it's pushed to a container registry (like Docker Hub).
8.  **Deployment to Cloud**: The Docker image is deployed to a cloud service (e.g., AWS EC2, Azure App Service) for public access.

---

## 🛠️ Tech Stack

-   **Programming Language**: Python 3.9
-   **Data Manipulation & ML**: Pandas, NumPy, Scikit-learn
-   **Web Framework**: Flask
-   **Containerization**: Docker
-   **CI/CD**: GitHub Actions
-   **Cloud Provider**: Amazon Web Services (AWS) - *Can be adapted for Azure, GCP, etc.*
-   **IDE**: Visual Studio Code

---

## 📂 Project Structure

The project follows a modular structure for better organization and scalability.

```
.
├── .github/workflows/         # GitHub Actions CI/CD pipeline
├── app.py                     # Flask application for predictions
├── dockerfile                 # Docker configuration
├── requirements.txt           # Project dependencies
├── setup.py                   # For creating the project as a package
├── src/
│   ├── __init__.py
│   ├── components/            # Individual pipeline components
│   │   ├── __init__.py
│   │   ├── data_ingestion.py
│   │   ├── data_transformation.py
│   │   └── model_trainer.py
│   ├── exception.py           # Custom exception handling
│   ├── logger.py              # Logging setup
│   ├── pipeline/              # Main execution pipelines
│   │   ├── __init__.py
│   │   ├── predict_pipeline.py
│   │   └── train_pipeline.py
│   └── utils.py               # Utility functions (e.g., saving objects)
└── notebooks/
    └── EDA_and_Training.ipynb # Jupyter notebook for experimentation
```

---

## ⚙️ How to Run the Project Locally

### Step 1: Clone the Repository

```bash
git clone [https://github.com/](https://github.com/)[YOUR_USERNAME]/[YOUR_REPO_NAME].git
cd [YOUR_REPO_NAME]
```

### Step 2: Create a Virtual Environment and Install Dependencies

It's recommended to use a virtual environment to manage dependencies.

```bash
# For Windows
python -m venv venv
.\venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

Now, install the required packages:

```bash
pip install -r requirements.txt
```

### Step 3: Run the Training Pipeline

To start the complete training pipeline, which includes data ingestion, transformation, and model training, run the following command from the root directory:

```bash
python src/pipeline/train_pipeline.py
```

After successful execution, a trained model will be saved in the `artifacts` directory.

### Step 4: Run the Prediction Web App

To start the Flask server and use the prediction interface, run:

```bash
python app.py
```

Open your web browser and navigate to `http://127.0.0.1:5000`. You should see the web interface where you can input data to get a prediction.

---

## 🤖 CI/CD with GitHub Actions

This project uses GitHub Actions for continuous integration and deployment. The workflow is defined in `.github/workflows/main.yml`.

-   **Trigger**: The pipeline is triggered on every `push` to the `main` branch.
-   **Jobs**:
    1.  **Build**: Sets up the Python environment, installs dependencies, and runs the training pipeline.
    2.  **Build and Push Docker Image**: If the build job is successful, it builds a Docker image from the `dockerfile` and pushes it to Docker Hub.

*(Note: You will need to configure `DOCKER_USERNAME` and `DOCKER_PASSWORD` as secrets in your GitHub repository settings for the Docker push to work.)*

---

## ☁️ Deployment

The application is containerized using Docker and is ready for deployment on any cloud platform that supports Docker containers, such as:

-   Amazon Web Services (AWS) EC2
-   Microsoft Azure App Service
-   Google Cloud Run
-   Heroku

The general steps for deployment involve pulling the Docker image from the registry and running it on the cloud instance.

---
## 📈 Model Evaluation

Here is a comparison of various regression models evaluated on both training and test sets using key metrics: RMSE (Root Mean Squared Error), MAE (Mean Absolute Error), and R² Score.

| Model                    | Dataset   | RMSE   | MAE    | R² Score |
|-------------------------|-----------|--------|--------|----------|
| **Linear Regression**   | Train     | 5.3244 | 4.2671 | 0.8743   |
|                         | Test      | 5.3960 | 4.2158 | 0.8803   |
| **Lasso Regression**    | Train     | 6.5938 | 5.2063 | 0.8071   |
|                         | Test      | 6.5197 | 5.1579 | 0.8253   |
| **Ridge Regression**    | Train     | 5.3233 | 4.2650 | 0.8743   |
|                         | Test      | 5.3904 | 4.2111 | 0.8806   |
| **KNN Regressor**       | Train     | 5.7077 | 4.5167 | 0.8555   |
|                         | Test      | 7.2530 | 5.6210 | 0.7838   |
| **Decision Tree**       | Train     | 0.2795 | 0.0187 | 0.9997   |
|                         | Test      | 7.7421 | 6.1100 | 0.7537   |
| **Random Forest**       | Train     | 2.2982 | 1.8193 | 0.9766   |
|                         | Test      | 5.9545 | 4.6169 | 0.8543   |
| **XGBRegressor**        | Train     | 1.0073 | 0.6875 | 0.9955   |
|                         | Test      | 6.4733 | 5.0577 | 0.8278   |
| **CatBoost Regressor**  | Train     | 3.0427 | 2.4054 | 0.9589   |
|                         | Test      | 6.0086 | 4.6125 | 0.8516   |
| **AdaBoost Regressor**  | Train     | 5.8873 | 4.8157 | 0.8463   |
|                         | Test      | 6.0281 | 4.6901 | 0.8507   |

### ✅ Observations

- **Ridge Regression** and **Linear Regression** offer a good balance between training and test performance with high R² scores and low error values.
- **Random Forest** and **CatBoost** also show strong generalization, though Random Forest slightly overfits.
- **Decision Tree** severely overfits — perfect train score but poor test performance.
- **XGBRegressor** shows excellent training results but is overfitting slightly.
- **KNN** underperforms on the test set relative to training.
- **Lasso** has comparatively lower performance, indicating it may be underfitting.

This indicates that the model can explain a significant portion of the variance in the student performance data.
