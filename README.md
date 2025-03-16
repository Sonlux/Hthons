Kubernetes AI Failure Predictor
This repository contains an AI-powered failure prediction system deployed on Kubernetes. The system utilizes machine learning models to analyze Prometheus metrics and predict failures in a Kubernetes environment.

📌 Project Structure
graphql
Copy
Edit
📂 K8/
 ├── __pycache__/                # Cached Python files
 ├── Dockerfile                  # Docker configuration
 ├── app.py                      # FastAPI application for predictions
 ├── fetch_metrics.py            # Script to fetch Prometheus metrics
 ├── k8s-deployment.yaml         # Kubernetes deployment configuration
 ├── k8s_failure_model.pkl       # Pretrained AI model
 ├── patch.json                  # Patch file for Kubernetes service updates
 ├── prometheus_data.csv         # Sample Prometheus data (CSV format)
 ├── prometheus_data.json        # Sample Prometheus data (JSON format)
 ├── train_model.py              # Model training script
 ├── README.md                   # Project documentation
🚀 Getting Started
1️⃣ Prerequisites
Minikube (for local Kubernetes cluster)
Docker
kubectl (Kubernetes CLI)
Python 3.x
Prometheus (for monitoring)
2️⃣ Setup & Deployment
🔹 Step 1: Build and Push Docker Image
sh
Copy
Edit
docker build -t ai-failure-predictor .
docker tag ai-failure-predictor <your-dockerhub-username>/ai-failure-predictor:latest
docker push <your-dockerhub-username>/ai-failure-predictor:latest
🔹 Step 2: Deploy to Kubernetes
sh
Copy
Edit
kubectl apply -f k8s-deployment.yaml
🔹 Step 3: Expose the Service
sh
Copy
Edit
kubectl patch svc ai-failure-predictor --type merge --patch '{"spec": {"type": "NodePort"}}'
🔹 Step 4: Access the API
sh
Copy
Edit
minikube service ai-failure-predictor --url
Visit the URL shown in the output.

📊 Fetching Prometheus Metrics
To collect Prometheus metrics, run:

sh
Copy
Edit
python fetch_metrics.py
📜 Model Training
If you want to retrain the AI model:

sh
Copy
Edit
python train_model.py
📮 API Endpoints
Method	Endpoint	Description
GET	/	Health check
POST	/predict	Predict system failures
Example request:

json
Copy
Edit
{
  "cpu_usage": 75.3,
  "memory_usage": 60.5,
  "disk_io": 20.1
}
👨‍💻 Contributors
Lakshan (@YourGitHubHandle)
📜 License
This project is licensed under the MIT License.
