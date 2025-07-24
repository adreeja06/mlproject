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

## 📈 Model Performance

The final model selected is a **Ridge Regression** model, which achieved the following performance on the test set:

-   **R-squared Score**: `[Enter Your R2 Score Here, e.g., 0.88]`
-   **Adjusted R-squared Score**: `[Enter Your Adjusted R2 Score Here]`

This indicates that the model can explain a significant portion of the variance in the student performance data.
