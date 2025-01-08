# FastAPI GCP Template

## Overview

Template for running a FastAPI app locally with Docker Compose and deploying to GCP.

---

## Prerequisites

- Docker
- Docker Compose

---

## Running Locally

1. **Set Up Environment Variables:**  
   Create a `.env` file from the example template and customize it:

   ```bash
   cp .env.example .env && code .env
   ```

2. **Build and Start:**

   ```bash
   docker-compose up --build
   ```

3. **Stop and Clean Up:**
   ```bash
   docker-compose down
   ```

---

## Deploying to GCP

1. **Set Up a Service Account (if needed):**  
   If you don’t have an existing service account:

   - Create one in the Google Cloud Console.
   - Assign these roles:
     - **Cloud Run Admin**
     - **Artifact Registry Administrator**
     - **Owner**
   - Download the JSON key for the account and add it to GitHub Secrets as `GCP_SERVICE_ACCOUNT_KEY`.

2. **Configure GitHub Workflow:**  
   Open the GitHub workflow configuration file and update the GCP variables:

   ```bash
   code .github/workflows/deploy.yml
   ```

3. **Trigger Deployment:**  
   Push your changes to GitHub. The workflow will deploy the application to Cloud Run.
