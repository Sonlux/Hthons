## **K8's Failure Predictor 🚀**  

### **📌 Overview**  
The **AI Failure Predictor** leverages **machine learning** and **Prometheus monitoring** to detect potential system failures in a **Kubernetes cluster** before they happen. This helps in **proactive maintenance** and **reducing downtime**.  

---

## **📂 Project Structure**  

```bash
K8/
│── Dockerfile                 # Docker setup for the application
│── app.py                      # Main API for prediction
│── fetch_metrics.py            # Script to fetch Prometheus metrics
│── k8s-deployment.yaml         # Kubernetes deployment configuration
│── k8s_failure_model.pkl       # Trained ML model
│── patch.json                  # Patch file for Kubernetes service
│── prometheus_data.csv         # Sample Prometheus metrics dataset
│── prometheus_data.json        # Prometheus data in JSON format
│── train_model.py              # Model training script
│── README.md                   # Project documentation
```

---

## **🚀 Installation & Setup**  

### **🔹 Prerequisites**  
Ensure you have the following installed:  
- **Docker**  
- **Kubernetes (kubectl, Minikube, or a cluster)**  
- **Python 3.8+**  
- **Prometheus for monitoring**  

### **🔹 Clone the Repository**  
```bash
git clone https://github.com/Sonlux/Hthons.git
cd Hthons/K8
```

### **🔹 Build & Run Docker Container**  
```bash
docker build -t ai-failure-predictor .
docker run -p 8000:8000 ai-failure-predictor
```

### **🔹 Deploy to Kubernetes**  
```bash
kubectl apply -f k8s-deployment.yaml
```

Check the status of the pod:  
```bash
kubectl get pods
```

Expose the service:  
```bash
kubectl expose deployment ai-failure-predictor --type=NodePort --port=8000
```

Find the service URL:  
```bash
minikube service ai-failure-predictor --url
```

---

## **🖥️ API Endpoints**  

| Endpoint            | Method | Description |
|---------------------|--------|-------------|
| `/predict`         | `POST` | Sends Prometheus data to predict failures |
| `/metrics`         | `GET`  | Fetches real-time Prometheus metrics |
| `/health`          | `GET`  | Checks if the API is running |

### **🔹 Example API Call**  
```bash
curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{"cpu_usage": 75, "memory_usage": 80, "disk_io": 50}'
```

---

## **📊 Monitoring with Prometheus & Grafana**  

1. **Start Prometheus**  
   ```bash
   prometheus --config.file=prometheus.yml
   ```
2. **Access Prometheus Dashboard**  
   ```
   http://localhost:9090
   ```
3. **Visualize Metrics in Grafana**  
   - Add Prometheus as a data source  
   - Create dashboards for monitoring  

---

## **⚙️ Patching the Service (NodePort)**  

If your service isn't accessible, patch it:  
```bash
kubectl patch svc ai-failure-predictor --type="merge" --patch='{"spec": {"type": "NodePort"}}'
```

To check the new port:  
```bash
kubectl get svc ai-failure-predictor
```

---

## **🤖 Model Training**  

To retrain the ML model:  
```bash
python train_model.py
```

---

## **🐛 Troubleshooting**  

| Issue | Solution |
|-------|----------|
| **Service not accessible** | Check if the service is exposed using `kubectl expose` |
| **Pod stuck in `Pending` state** | Run `kubectl describe pod <pod-name>` for details |
| **Docker build issues** | Ensure Docker daemon is running |

---

## **🔮 Future Enhancements**  
✅ **Multi-cluster support**  
✅ **Real-time alerting with Prometheus**  
✅ **More advanced ML models for failure prediction**  

---

## **📜 License**  
This project is licensed under the **MIT License**.  

---

