# AI Anime Recommender: Personalized Anime Discovery System


[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-blue?logo=github)](https://github.com/HamzaImtiaz03/Anime_Recommender_AI_System)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?logo=docker)](https://www.docker.com/)
[![Kubernetes Deployed](https://img.shields.io/badge/Deployed-Kubernetes-orange?logo=kubernetes)](https://kubernetes.io/)
[![GCP Hosted](https://img.shields.io/badge/Hosted-GCP-brightgreen?logo=google-cloud)](https://cloud.google.com/)

## Overview

The **AI Anime Recommender** is an innovative recommendation engine that leverages artificial intelligence to deliver personalized anime suggestions based on user preferences, genres, ratings, and semantic similarities. Powered by advanced NLP and vector embeddings, it processes anime datasets to generate accurate, context-aware recommendations, making it a must-have tool for anime enthusiasts, content platforms, and media recommendation systems.

Built with a focus on scalability and observability, this project integrates state-of-the-art AI frameworks with robust DevOps practices. It features a Streamlit-based interactive web interface for seamless user experiences, containerized deployment on Kubernetes, and real-time monitoring via Grafana Cloud. Whether you're discovering new anime or building AI-driven media apps, this system combines efficiency, accuracy, and enterprise-grade deployment.

## Key Features

- **AI-Driven Recommendations**: Utilizes LangChain for chaining NLP tasks, Groq for fast inference, Hugging Face embeddings for semantic search, and ChromaDB for efficient vector storage and retrieval.
- **Data Processing Pipeline**: Loads and processes anime datasets (e.g., via Pandas), generates embeddings, and trains recommender models for personalized suggestions.
- **Interactive Frontend**: Streamlit app for user-friendly querying, visualization of recommendations, and real-time interactions.
- **Custom Configurations**: Supports logging, custom exceptions, and environment variables for secure API key management.
- **Containerization & Orchestration**: Dockerized for portability, deployed on Kubernetes (via Minikube) for scalability and high availability.
- **Cloud Deployment**: Hosted on Google Cloud Platform (GCP) VM instances with Kubernetes integration.
- **Monitoring & Observability**: Grafana Cloud for cluster metrics, resource usage, and performance insights.
- **CI/CD Readiness**: GitHub integration for code versioning, with Helm charts for streamlined Kubernetes deployments.

## Architecture

The project employs a modular architecture, from data ingestion to deployment and monitoring, as illustrated below:

![Project Architecture Flowchart](AI+Anime+Recommender+Workflow.png) <!-- Replace with actual image URL or embed -->

### High-Level Breakdown:
1. **Project Setup**: Groq/Hugging Face API integration, virtual environment, logging, custom exceptions, and structured configurations.
2. **Core Code**: Data loaders, ChromaDB vector database, prompt templates, recommender class for training and inference.
3. **Application Layer**: Streamlit app for frontend interactions.
4. **Deployment**: Dockerfile for containerization, Kubernetes YAML for deployments/services, GCP VM hosting, Minikube for local K8s, and GitHub for versioning.
5. **Monitoring**: Grafana Cloud integration via Helm charts for observability.

This design ensures seamless workflows, fault tolerance, and easy extensibility for additional datasets or features.

## Technologies Used

- **AI/ML Frameworks**: LangChain (core, community, Groq integration, Hugging Face), Sentence-Transformers (embeddings), ChromaDB (vector database).
- **Data Handling**: Pandas (data processing), Python-dotenv (environment management).
- **Frontend**: Streamlit (interactive web apps).
- **Containerization & Orchestration**: Docker (containerization), Kubernetes (via Minikube), Helm (for Grafana integration).
- **Cloud & Monitoring**: Google Cloud Platform (GCP VM), Grafana Cloud (observability).
- **Version Control**: GitHub.

Full dependencies are listed in `requirements.txt`.

## Installation

### Prerequisites
- Python 3.10+
- Git
- Docker (for containerization)
- Google Cloud Platform Account (for deployment)
- API Keys: Groq and Hugging Face (stored in `.env`)
- Optional: Minikube and kubectl for local Kubernetes testing

### Steps
1. **Clone the Repository**:
   ```
   git clone https://github.com/HamzaImtiaz03/Anime_Recommender_AI_System.git
   cd Anime_Recommender_AI_System
   ```

2. **Set Up Virtual Environment** (Recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Unix/Mac
   # Or on Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```
   pip install -e .
   ```

4. **Configure Environment Variables**:
   Create a `.env` file in the root directory:
   ```
   GROQ_API_KEY=your_groq_api_key
   HUGGINGFACEHUB_API_TOKEN=your_huggingface_token
   # Add other variables as needed
   ```

5. **Prepare Dataset**:
   Place anime datasets (e.g., CSV files with titles, genres, ratings) in the appropriate data directory. The system will load and process them automatically.

## Usage

1. **Run the Application Locally**:
   ```
   streamlit run app/app.py
   ```
   - Access the recommender at `http://localhost:8501`.
   - Input preferences (e.g., favorite anime, genres) and receive tailored recommendations.

2. **Query Examples**:
   - "Recommend anime similar to 'Attack on Titan'."
   - "Top romance anime with high ratings."
   - The system retrieves embeddings from ChromaDB, computes similarities, and generates suggestions via Groq-powered prompts.

3. **Customization**:
   - Adjust recommender parameters in the core classes.
   - Extend with new datasets or integrate additional ML models.

## Deployment

This project supports local, containerized, and cloud-based deployments with Kubernetes for orchestration and Grafana for monitoring.

### Prerequisites
- GCP VM Instance (configured as per `FULL_DOCUMENTATION.md`).
- Minikube and Helm installed on the VM.
- Kubernetes secrets for API keys.

### Pipeline Overview
1. **Build Docker Image**: Use the `Dockerfile` to create a production-ready image.
2. **Deploy to Kubernetes**: Apply `llmops-k8s.yaml` for Deployment and LoadBalancer Service.
3. **Set Up Monitoring**: Install Grafana Cloud via Helm charts in the `monitoring` namespace.
4. **Access the App**: Use Minikube tunnel and port-forwarding to expose the app externally.

### Detailed Steps
- Follow `FULL_DOCUMENTATION.md` for GCP VM setup, Docker/Minikube installation, Kubernetes deployment, and Grafana integration.
- Build and run Docker image locally:
  ```
  docker build -t anime-recommender .
  docker run -p 8501:8501 anime-recommender
  ```
- Deploy to GCP Kubernetes:
  ```
  kubectl create secret generic llmops-secrets --from-literal=GROQ_API_KEY=your_key --from-literal=HUGGINGFACEHUB_API_TOKEN=your_token
  kubectl apply -f llmops-k8s.yaml
  minikube tunnel  # In one terminal
  kubectl port-forward svc/llmops-service 8501:80 --address 0.0.0.0  # In another
  ```
- Monitor via Grafana Cloud dashboard for cluster metrics.

Once deployed, access the app via the external IP on port 8501.

## Contributing

We welcome contributions to enhance recommendations, add features, or improve deployment! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit changes (`git commit -m 'Add YourFeature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a Pull Request.

Ensure code follows best practices and includes relevant tests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Frameworks: LangChain, Hugging Face, Groq, ChromaDB.
- Tools: Streamlit, Docker, Kubernetes, Minikube, Grafana Cloud, GCP.
- Inspired by AI-driven recommendation systems in entertainment and media.

For questions or support, open an issue on GitHub or contact [Hamza Imtiaz](mailto:your.hamzaimtiaz8668@example.com).

---

*Built by Hamza Imtiaz | Unlocking Your Next Anime Adventure with AI*