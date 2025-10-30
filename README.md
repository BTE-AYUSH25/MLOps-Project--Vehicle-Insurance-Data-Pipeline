

# 🚗 Vehicle Insurance Prediction - MLOps End-to-End Project

[![CI/CD Pipeline](https://github.com/BTE-AYUSH25/MLOps-Project--Vehicle-Insurance-Data-Pipeline/actions/workflows/ci-cd-free.yaml/badge.svg)](https://github.com/BTE-AYUSH25/MLOps-Project--Vehicle-Insurance-Data-Pipeline/actions)
[![Live Demo](https://img.shields.io/badge/Live-Demo-brightgreen)](https://vehicle-ml-app.onrender.com)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104.1-green.svg)](https://fastapi.tiangolo.com/)

A complete MLOps pipeline for predicting vehicle insurance purchases using machine learning. This project demonstrates end-to-end ML lifecycle management with automated CI/CD deployment.


## 📋 Project Overview

This project predicts whether a customer will purchase vehicle insurance based on their demographic and vehicle information. It implements a full MLOps pipeline with:

- **Data Ingestion** from MongoDB
- **Automated Model Training** with Random Forest
- **REST API** with FastAPI
- **CI/CD Pipeline** with GitHub Actions
- **Cloud Deployment** on Render 
- **Monitoring & Logging**

## 🏗️ Architecture

```
Raw Data → MongoDB → Data Validation → Feature Engineering → Model Training → FastAPI → Web Interface
                                     ↓
                CI/CD Pipeline (GitHub Actions + Render/AWS)
```

## 🚀 Quick Start

### Prerequisites
- Python 3.10
- MongoDB Atlas account
- GitHub account
- Render account (for free deployment)
 -AWS (optional)

### Local Development

1. **Clone the repository**
```bash
git clone https://github.com/BTE-AYUSH25/MLOps-Project--Vehicle-Insurance-Data-Pipeline.git
cd your-repo-name
```

2. **Create virtual environment**
```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
```bash
# For macOS/Linux
export MONGODB_URL="your_mongodb_connection_string"

# For Windows PowerShell
$env:MONGODB_URL="your_mongodb_connection_string"
```

5. **Run the application locally**
```bash
python app.py
# or
uvicorn app:app --host 0.0.0.0 --port 5000
```

Visit `http://localhost:5000` to see the application.

## 📊 Dataset

The dataset contains customer information for vehicle insurance with the following features:

| Feature | Description | Type |
|---------|-------------|------|
| Gender | Customer gender | Categorical |
| Age | Customer age | Numerical |
| Driving_License | Whether customer has driving license | Binary |
| Region_Code | Unique code for customer region | Numerical |
| Previously_Insured | Whether customer already has insurance | Binary |
| Vehicle_Age | Age of the vehicle | Categorical |
| Vehicle_Damage | Whether customer had vehicle damage | Binary |
| Annual_Premium | Yearly insurance premium amount | Numerical |
| Policy_Sales_Channel | Sales channel code | Numerical |
| Vintage | Number of days as customer | Numerical |
| Response | Target variable (1: Interested, 0: Not Interested) | Binary |

## 🔧 Project Structure

```
MLOps-Project--Vehicle-Insurance-Data-Pipeline/
├── .github/workflows/          # CI/CD pipelines
│   ├── ci-cd-free.yaml        # Free tier deployment
│   └── ci-cd-aws.yaml         # AWS deployment (demo)
├── src/                       # Source code
│   ├── components/            # ML pipeline components
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   ├── pipeline/              # Training & prediction pipelines
│   ├── entity/                # Configuration entities
│   ├── constants/             # Project constants
│   ├── utils/                 # Utility functions
│   ├── logger.py              # Logging configuration
│   └── exception.py           # Exception handling
├── templates/                 # HTML templates
│   └── vehicledata.html
├── static/                    # CSS and static files
│   └── css/style.css
├── config/                    # Configuration files
│   ├── schema.yaml
│   └── model.yaml
├── notebooks/                 # Jupyter notebooks for EDA
├── app.py                     # FastAPI application
├── demo.py                    # Demo script
├── requirements.txt           # Python dependencies
├── Dockerfile                 # Container configuration
├── render.yaml               # Render deployment config
└── pyproject.toml            # Project metadata
```

## 🛠️ ML Pipeline Components

### 1. Data Ingestion
- Connects to MongoDB Atlas
- Exports data to feature store
- Splits data into train/test sets

### 2. Data Validation
- Validates schema compliance
- Checks for missing values
- Generates validation reports

### 3. Data Transformation
- Handles categorical encoding
- Applies feature scaling
- Uses SMOTEENN for imbalance handling

### 4. Model Training
- Random Forest Classifier
- Hyperparameter tuning
- Model evaluation metrics

### 5. Model Deployment
- FastAPI web interface
- Real-time predictions
- Model versioning

## 🌐 API Endpoints

| Endpoint | Method | Description |
|----------|---------|-------------|
| `/` | GET | Web interface for predictions |
| `/` | POST | Submit form data for prediction |
| `/train` | GET | Trigger model training pipeline |

### Example Prediction Request
```python
import requests

data = {
    "Gender": 1,
    "Age": 44,
    "Driving_License": 1,
    "Region_Code": 28.0,
    "Previously_Insured": 0,
    "Annual_Premium": 40454.0,
    "Policy_Sales_Channel": 26.0,
    "Vintage": 217,
    "Vehicle_Age_lt_1_Year": 0,
    "Vehicle_Age_gt_2_Years": 1,
    "Vehicle_Damage_Yes": 1
}

response = requests.post("https://vehicle-ml-app.onrender.com", json=data)
print(response.json())
```

## 🔄 CI/CD Pipeline

This project implements two CI/CD strategies:

### 1. Free Tier Deployment (Primary)
- **Trigger**: Push to `main` branch
- **Platform**: Render + GitHub Actions
- **Cost**: $0/month
- **Auto-deploy**: Yes

### 2. AWS Deployment (Demo)
- **Trigger**: Manual on `aws-demo` branch  
- **Platform**: EC2 + ECR + GitHub Self-hosted runner
- **Cost**: Pay-per-use (for demo only)

## 🚀 Deployment Guide

### Free Deployment (Recommended)
1. Fork this repository
2. Create account on [Render.com](https://render.com)
3. Connect your GitHub repository
4. Deploy as Web Service
5. Your app will auto-deploy on every git push

### AWS Deployment (Advanced)
Follow the detailed steps in `projectflow.txt` for AWS setup.

## 📈 Model Performance

| Metric | Score |
|--------|-------|
| Accuracy | ~85% |
| F1-Score | ~0.931 |
| Precision | ~0.882 |
| Recall | ~0.985 |

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Check your connection string
   - Verify IP is whitelisted in MongoDB Atlas
   - Ensure database and collection names match

2. **Build Failures on Render**
   - Check `requirements.txt` for missing dependencies
   - Verify Dockerfile commands
   - Check application logs in Render dashboard

3. **Import Errors**
   - Ensure virtual environment is activated
   - Run `pip install -e .` for local package installation

## 🤝 Contributing

We welcome contributions! Please feel free to submit pull requests or open issues for bugs and feature requests.

### Development Setup
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- FastAPI documentation and community
- Render for free tier hosting


## 📞 Contact
 
- GitHub: [@BTE-AYUSH25](https://github.com/BTE-AYUSH25)
- Email: ayushjee2155@gmail.com
- [ LinkedIn](https://www.linkedin.com/in/anm692369/)

---

**⭐ Don't forget to star this repository if you found it helpful!**

---
------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------
