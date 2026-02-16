# 🚀 MLOps - Machine Learning Operations

Deploy, monitor, and maintain ML models in production. **Perfect for Full Stack Developers with DevOps experience.**

## 🎯 What is MLOps?

MLOps = Machine Learning + DevOps

It's the practice of deploying, monitoring, and maintaining ML models in production, just like you do with web applications.

**Why MLOps?**
- Most ML projects fail to reach production (85%)
- Models in Jupyter notebooks ≠ Production-ready systems
- ML models need continuous monitoring and retraining
- **High demand**: Companies need ML in production, not just experiments

---

## 💼 Why MLOps is Perfect for You

With your background (7+ YOE, AWS/GCP, Kubernetes, CI/CD):

✅ **You already know**:
- Docker, Kubernetes
- CI/CD pipelines
- Cloud infrastructure (AWS/GCP)
- API development
- Monitoring and logging

✅ **You need to learn**:
- ML model training and evaluation
- Model serving and inference
- ML-specific tools (MLflow, Kubeflow)
- Model monitoring and drift detection

**Result**: 6 months to become MLOps Engineer vs 12+ months for pure ML Engineer

---

## 🏗️ MLOps Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    MLOps Pipeline                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Data Pipeline                                          │
│     ├── Data Collection (APIs, Databases, Streams)        │
│     ├── Data Validation                                    │
│     └── Feature Engineering                                │
│                                                             │
│  2. Model Training                                         │
│     ├── Experiment Tracking (MLflow)                       │
│     ├── Hyperparameter Tuning                              │
│     └── Model Versioning                                   │
│                                                             │
│  3. Model Deployment                                       │
│     ├── Model Registry                                     │
│     ├── A/B Testing                                        │
│     └── Canary Deployment                                  │
│                                                             │
│  4. Model Serving                                          │
│     ├── REST API (FastAPI, Flask)                          │
│     ├── Batch Inference                                    │
│     └── Real-time Inference                                │
│                                                             │
│  5. Monitoring                                             │
│     ├── Performance Metrics                                │
│     ├── Model Drift Detection                              │
│     └── Data Drift Detection                               │
│                                                             │
│  6. CI/CD                                                  │
│     ├── Automated Testing                                  │
│     ├── Automated Retraining                               │
│     └── Automated Deployment                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🛠️ MLOps Tech Stack

### Your Existing Skills (Leverage These):
```yaml
Cloud: AWS (SageMaker, Lambda, ECR), GCP (Vertex AI, Cloud Run)
Containers: Docker, Kubernetes
Orchestration: Kubernetes, Docker Compose
CI/CD: GitHub Actions, Jenkins
Monitoring: Prometheus, Grafana
APIs: REST, Node.js, Express
Databases: MongoDB, SQL
```

### New Tools to Learn:
```yaml
ML Frameworks:
  - TensorFlow / PyTorch (model training)
  - scikit-learn (classical ML)

Model Serving:
  - TensorFlow Serving
  - TorchServe
  - FastAPI (Python REST API)
  - Seldon Core (Kubernetes-native)

Experiment Tracking:
  - MLflow (most popular)
  - Weights & Biases
  - Neptune.ai

ML Orchestration:
  - Kubeflow Pipelines
  - Apache Airflow (you might know this)
  - Prefect

Model Monitoring:
  - Evidently AI (drift detection)
  - WhyLabs
  - Prometheus + Grafana (you know this!)

Data Versioning:
  - DVC (Data Version Control)
  - Pachyderm

Feature Stores:
  - Feast
  - Tecton
```

---

## 📚 Learning Path (Months 5-6)

### Week 1-2: Model Serving with FastAPI

**Goal**: Serve ML models as REST APIs

```python
# app.py
from fastapi import FastAPI
import joblib
import numpy as np
from pydantic import BaseModel

app = FastAPI()

# Load model at startup
model = joblib.load('model.pkl')

class PredictionInput(BaseModel):
    features: list[float]

class PredictionOutput(BaseModel):
    prediction: float
    probability: float

@app.post("/predict", response_model=PredictionOutput)
def predict(input_data: PredictionInput):
    # Convert to numpy array
    X = np.array(input_data.features).reshape(1, -1)

    # Predict
    prediction = model.predict(X)[0]
    probability = model.predict_proba(X)[0].max()

    return {
        "prediction": float(prediction),
        "probability": float(probability)
    }

@app.get("/health")
def health():
    return {"status": "healthy"}
```

```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

```bash
# Build and run
docker build -t ml-api .
docker run -p 8000:8000 ml-api

# Test
curl -X POST "http://localhost:8000/predict" \
  -H "Content-Type: application/json" \
  -d '{"features": [1.0, 2.0, 3.0]}'
```

**Practice**:
- [ ] Build FastAPI app for ML model
- [ ] Dockerize the application
- [ ] Deploy to Cloud Run / AWS Lambda
- [ ] Add logging and error handling

---

### Week 3-4: Experiment Tracking with MLflow

**Goal**: Track experiments, parameters, and models

```python
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# Start MLflow tracking
mlflow.set_experiment("customer-churn")

with mlflow.start_run():
    # Log parameters
    n_estimators = 100
    max_depth = 10
    mlflow.log_param("n_estimators", n_estimators)
    mlflow.log_param("max_depth", max_depth)

    # Train model
    model = RandomForestClassifier(n_estimators=n_estimators, max_depth=max_depth)
    model.fit(X_train, y_train)

    # Evaluate
    predictions = model.predict(X_test)
    accuracy = accuracy_score(y_test, predictions)

    # Log metrics
    mlflow.log_metric("accuracy", accuracy)

    # Log model
    mlflow.sklearn.log_model(model, "model")

    # Log artifacts (plots, data)
    plt.savefig("confusion_matrix.png")
    mlflow.log_artifact("confusion_matrix.png")
```

```bash
# Start MLflow UI
mlflow ui --port 5000

# View experiments at http://localhost:5000
```

**Practice**:
- [ ] Track experiments with different parameters
- [ ] Compare model performance in MLflow UI
- [ ] Register best model in Model Registry
- [ ] Load model from registry for deployment

---

### Week 5-6: Kubernetes Deployment

**Goal**: Deploy ML model to Kubernetes

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-model
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-model
  template:
    metadata:
      labels:
        app: ml-model
    spec:
      containers:
      - name: ml-api
        image: your-registry/ml-api:latest
        ports:
        - containerPort: 8000
        resources:
          requests:
            memory: "512Mi"
            cpu: "500m"
          limits:
            memory: "1Gi"
            cpu: "1000m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: ml-service
spec:
  selector:
    app: ml-model
  ports:
  - port: 80
    targetPort: 8000
  type: LoadBalancer
```

```bash
# Deploy
kubectl apply -f deployment.yaml

# Check status
kubectl get pods
kubectl get services

# Scale
kubectl scale deployment ml-model --replicas=5
```

**Practice**:
- [ ] Deploy ML API to Kubernetes
- [ ] Setup autoscaling (HPA)
- [ ] Add Prometheus monitoring
- [ ] Configure Ingress with SSL

---

### Week 7-8: ML Pipelines with Kubeflow

**Goal**: Automate end-to-end ML workflow

```python
from kfp import dsl
from kfp import compiler

@dsl.component
def load_data() -> str:
    """Load and prepare data"""
    import pandas as pd

    # Load data
    df = pd.read_csv('s3://bucket/data.csv')

    # Save processed data
    df.to_csv('/data/processed.csv')
    return '/data/processed.csv'

@dsl.component
def train_model(data_path: str) -> str:
    """Train ML model"""
    import pandas as pd
    from sklearn.ensemble import RandomForestClassifier
    import joblib

    # Load data
    df = pd.read_csv(data_path)
    X = df.drop('target', axis=1)
    y = df['target']

    # Train
    model = RandomForestClassifier()
    model.fit(X, y)

    # Save model
    joblib.dump(model, '/models/model.pkl')
    return '/models/model.pkl'

@dsl.component
def deploy_model(model_path: str):
    """Deploy model to production"""
    # Deploy logic here
    pass

@dsl.pipeline(name='ml-training-pipeline')
def ml_pipeline():
    load_task = load_data()
    train_task = train_model(data_path=load_task.output)
    deploy_task = deploy_model(model_path=train_task.output)

# Compile pipeline
compiler.Compiler().compile(ml_pipeline, 'pipeline.yaml')
```

**Practice**:
- [ ] Build Kubeflow pipeline
- [ ] Schedule automatic retraining
- [ ] Add data validation step
- [ ] Implement A/B testing

---

### Week 9-10: Model Monitoring & Drift Detection

**Goal**: Monitor model performance in production

```python
from evidently import ColumnMapping
from evidently.report import Report
from evidently.metric_preset import DataDriftPreset, DataQualityPreset

# Reference data (training data)
reference_data = pd.read_csv('train_data.csv')

# Current production data
current_data = pd.read_csv('production_data.csv')

# Create drift report
report = Report(metrics=[
    DataDriftPreset(),
    DataQualityPreset()
])

report.run(reference_data=reference_data, current_data=current_data)

# Save HTML report
report.save_html('drift_report.html')

# Get drift metrics programmatically
drift_metrics = report.as_dict()

# Alert if drift detected
if drift_metrics['metrics'][0]['result']['dataset_drift']:
    print("⚠️ Data drift detected! Retrain model.")
    # Trigger retraining pipeline
```

**Monitoring Dashboard** (Prometheus + Grafana):
```python
from prometheus_client import Counter, Histogram, Gauge
import time

# Metrics
prediction_counter = Counter('ml_predictions_total', 'Total predictions')
prediction_latency = Histogram('ml_prediction_latency_seconds', 'Prediction latency')
model_accuracy = Gauge('ml_model_accuracy', 'Model accuracy')

@app.post("/predict")
def predict(input_data):
    start_time = time.time()

    # Make prediction
    prediction = model.predict(input_data)

    # Record metrics
    prediction_counter.inc()
    prediction_latency.observe(time.time() - start_time)

    return prediction
```

**Practice**:
- [ ] Setup Evidently for drift detection
- [ ] Create Grafana dashboard for ML metrics
- [ ] Implement alerting (Slack/Email)
- [ ] Setup automatic retraining on drift

---

### Week 11-12: CI/CD for ML

**Goal**: Automated testing and deployment

```yaml
# .github/workflows/ml-pipeline.yml
name: ML CI/CD Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest tests/

      - name: Data validation
        run: python scripts/validate_data.py

      - name: Model testing
        run: python scripts/test_model.py

  train:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Train model
        run: python train.py

      - name: Evaluate model
        run: python evaluate.py

      - name: Upload model artifact
        uses: actions/upload-artifact@v3
        with:
          name: model
          path: models/

  deploy:
    needs: train
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Download model
        uses: actions/download-artifact@v3

      - name: Build Docker image
        run: docker build -t ml-api:${{ github.sha }} .

      - name: Push to registry
        run: docker push ml-api:${{ github.sha }}

      - name: Deploy to Kubernetes
        run: |
          kubectl set image deployment/ml-model \
            ml-api=ml-api:${{ github.sha }}
```

**Practice**:
- [ ] Setup GitHub Actions for ML
- [ ] Automated model testing
- [ ] Automated deployment on model improvement
- [ ] Rollback strategy for failed deployments

---

## 🏋️ MLOps Projects

### Project 1: ML API with Monitoring
**Stack**: FastAPI + Docker + Prometheus + Grafana
- Build ML API
- Dockerize application
- Add Prometheus metrics
- Create Grafana dashboard
- Deploy to Cloud Run

### Project 2: Complete MLOps Pipeline
**Stack**: MLflow + Kubeflow + Kubernetes
- Data ingestion pipeline
- Experiment tracking with MLflow
- Model registry
- Automated deployment
- A/B testing setup

### Project 3: Real-time Fraud Detection
**Stack**: Kafka + ML + Kubernetes
- Stream data with Kafka
- Real-time inference
- Model monitoring
- Automated retraining
- Alert system

---

## 📊 MLOps Maturity Levels

**Level 0**: Manual process (Jupyter notebooks)
- ❌ No automation
- ❌ Manual deployment

**Level 1**: ML Pipeline Automation
- ✅ Automated training
- ❌ Manual deployment

**Level 2**: CI/CD Pipeline Automation
- ✅ Automated training
- ✅ Automated deployment
- ✅ Monitoring

**Goal**: Reach Level 2 in 6 months

---

## 💼 MLOps Job Requirements

Typical MLOps Engineer job posting:

**Required**:
- ✅ Python programming (you'll learn)
- ✅ Docker & Kubernetes (you know!)
- ✅ CI/CD pipelines (you know!)
- ✅ Cloud platforms (you know AWS/GCP!)
- ✅ ML fundamentals (you'll learn)
- ✅ REST APIs (you know!)

**Preferred**:
- MLflow or similar
- Kubeflow or Airflow
- Model serving (TensorFlow Serving)
- Monitoring (Prometheus/Grafana) (you know!)

**You already have 70% of requirements!**

---

## 📚 Best Resources

### Courses:
- **Full Stack Deep Learning** - Production ML
- **Made With ML** - MLOps best practices
- **Coursera: MLOps Specialization** by Andrew Ng

### Books:
- **Designing Machine Learning Systems** by Chip Huyen
- **Building Machine Learning Powered Applications** by Emmanuel Ameisen

### Communities:
- MLOps Community (Slack)
- r/MLOps (Reddit)
- MLOps.community website

---

## ✅ MLOps Checklist

- [ ] Built ML API with FastAPI
- [ ] Dockerized ML application
- [ ] Deployed to Kubernetes
- [ ] Setup MLflow experiment tracking
- [ ] Created ML pipeline (Kubeflow/Airflow)
- [ ] Implemented model monitoring
- [ ] Setup drift detection
- [ ] Built CI/CD for ML
- [ ] Created 2+ production-ready ML projects
- [ ] Contributed to MLOps open-source

---

## 🎯 6-Month MLOps Roadmap

**Months 1-4**: ML Fundamentals (required foundation)
**Months 5-6**: MLOps Focus

### Your Competitive Advantage:
```
Traditional ML Engineer → MLOps: 12-18 months
You (DevOps background) → MLOps: 6-9 months
```

---

[⬅️ Back to AI/ML](../)
