# FastAPI GCP Template

## Overview

Template for running a FastAPI app locally with Docker Compose and deploying to GCP.

---

## Prerequisites

- **Python** – Required to create a virtual environment and run the application.
- **Docker** – Needed for containerizing the FastAPI app.
- **Docker Compose** – Used to orchestrate and run the Docker containers during local development.
- **Google Cloud Account** – For deploying the application to Google Cloud.

---

## Running Locally

1. **Set Up Environment Variables:**  
   Create a `.env` file from the example template and customize it:

   ```bash
   cp .env.example .env && code .env
   ```

2. **Create and Activate Virtual Environment:**  
   Create a Python virtual environment:

   ```bash
   python -m venv .venv
   ```

   Then activate it:

   - **On macOS/Linux:**
     ```bash
     source .venv/bin/activate
     ```
   - **On Windows:**
     ```bash
     .venv\Scripts\activate
     ```

3. **Install Dependencies:**  
   With the virtual environment active, install the required packages:

   ```bash
   pip install -r requirements.txt
   ```

4. **Build and Start Docker Containers:**  
   Run the following command to build and run the Docker containers:

   ```bash
   docker-compose up --build
   ```

5. **Stop and Clean Up:**  
   To stop and remove the Docker containers, run:
   ```bash
   docker-compose down
   ```

---

## Deploying to GCP

1. **Set Up Google Cloud**

   - Select or Create a **Google Cloud Project** in Google Cloud Console.
   - Enable the following APIs:
     - **Cloud Run API**
     - **Artifact Registry API**
     - **Cloud Build API**
   - Select or Create a **Service Account** under **IAM & Admin > Service Accounts**, and assign these roles:
     - **Cloud Run Admin**
     - **Artifact Registry Administrator**
     - **Owner**
   - Generate a **JSON Key** under the Keys tab > Create new key > JSON, then download it.

2. **Add GitHub Secrets**  
   Go to your GitHub repository > Settings > Secrets and variables > Actions, and add the following:

   - `GCP_SERVICE_ACCOUNT_KEY`: Paste the contents of your downloaded JSON key file.
   - `GCP_PROJECT_ID`: Find this in the `project_id` field of `GCP_SERVICE_ACCOUNT_KEY`.
   - `GCP_ARTIFACT_REGISTRY_DOMAIN`: Check in Artifact Registry (e.g., `us-central1-docker.pkg.dev`).
   - `GCP_DEPLOY_REGION`: Choose a Cloud Run region (e.g., `us-central1`).

3. **Deploy**  
   Push your changes to the **main** branch:

   ```bash
   git add .
   git commit -m "Deploy update"
   git push origin main
   ```

   This triggers the **GitHub Actions workflow**, deploying the app to **Cloud Run**.
