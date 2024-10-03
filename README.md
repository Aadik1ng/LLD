
# Lung Cancer Detection Project

## Overview
This project aims to detect lung cancer from CT scan images using a Convolutional Neural Network (CNN). The model classifies the images into three categories: Normal, Benign, and Malignant. The project leverages MLOps tools like MLflow, ZenML, DVC, and GitHub for efficient and reproducible development and deployment.

## How to Setup and Run the Code

### Prerequisites
- Python 3.6 or later
- Pip (Python package installer)
- Virtual environment (recommended)

### Installation
1. **Clone the repository**:
    ```sh
    git clone https://github.com/Aadik1ng/LLD
    cd LLD
    ```

2. **Create a virtual environment and activate it**:
    ```sh
    python -m venv [Environment_name]
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. **Install the required packages**:
    ```sh
    pip install -r requirements.txt
    ```

### Running the Code
1. **Data Preparation**:
    Make sure your data is organized in the following structure:
    ```
    ./LLD/data/raw/
    ├── Bengin cases
    ├── Malignant cases
    └── Normal cases
    ```

2. **Data Version Control (DVC)**:
    Initialize DVC and set up remote storage:
    ```sh
    dvc init
    dvc remote add -d myremote <remote-storage-url>  #S3 or local
    dvc add ./data/raw
    dvc push
    ```

3. **Training the Model**:
    Run the training script to train the model and log experiments using MLflow:
    ```sh
    python train.py --data-dir ./LLD/data/raw --output-dir ./LLD/models
    ```

4. **Evaluating the Model**:
    Evaluate the trained model and log metrics:
    ```sh
    python evaluate.py --model-path ./LLD/models/lung_cancer_model.h5 --data-dir ./LLD/data/raw
    ```

5. **Inference**:
    Use the inference script to classify a new CT scan image:
    ```sh
    python inference.py --image-path <path-to-your-image>.jpg --model-path ./LLD/models/lung_cancer_model.h5
    ```

6. **Running the Streamlit App**:
    Launch the Streamlit app for interactive predictions:
    ```sh
    streamlit run app.py
    ```

## Model Performance
The model's performance is evaluated using the following metrics:
- **Accuracy**: 99%
- **Precision**: 
  - Normal cases: 1.00
  - Benign cases: 1.00
  - Malignant cases: 0.99
- **Recall**: 
  - Normal cases: 0.98
  - Benign cases: 1.00
  - Malignant cases: 1.00
- **F1-Score**: 
  - Normal cases: 0.99
  - Benign cases: 1.00
  - Malignant cases: 0.99
- **AUC (Area Under Curve)**: The AUC was not calculated as the ROC curve is typically used for binary classification, but the overall performance metrics suggest a high discriminative capability.
- **Confusion Matrix**:
    ```
    [[59, 0, 1],
     [0, 18, 0],
     [0, 0, 87]]
    ```

## Technical Challenges
Developing a lung cancer detection model involves several challenges:
- **Data Preprocessing**: Handling and preprocessing large volumes of medical imaging data.
- **Model Training**: Choosing the right architecture and hyperparameters for the CNN.
- **Evaluation**: Ensuring the model's performance is robust and generalizes well to unseen data.
- **MLOps Integration**: Efficiently managing the lifecycle of machine learning models using tools like MLflow, ZenML, and DVC.

## Importance of the Project
Lung cancer is one of the leading causes of cancer-related deaths worldwide. Early detection significantly improves the chances of successful treatment and survival. This project demonstrates how machine learning can aid in the early detection of lung cancer, potentially saving lives and reducing healthcare costs.

## MLOps Tools Used

### MLflow
MLflow is used for tracking and managing the machine learning experiments. It allows us to log parameters, metrics, and artifacts, ensuring reproducibility and easy comparison of different experiments.

### ZenML
ZenML is used for orchestrating machine learning pipelines. It simplifies the process of building, deploying, and managing ML workflows, ensuring that each step in the pipeline is executed efficiently and correctly.

### DVC (Data Version Control)
DVC is used for versioning the datasets and model files. It helps in tracking changes to data and models, enabling reproducibility and collaboration across different team members.

### GitHub
GitHub is used for version control and collaboration on the project's codebase. It allows multiple contributors to work on the project simultaneously, ensuring that changes are tracked and managed efficiently.

## Conclusion
This project highlights the integration of machine learning and MLOps tools to build a robust lung cancer detection model. The use of MLflow, ZenML, DVC, and GitHub ensures that the development process is efficient, reproducible, and scalable.
