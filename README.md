# CSP Lab 5: Deploying a Full-Stack Web Application to Azure

This repository contains the solution for **Cloud Service Provisioning (CSP) Lab 5**, showcasing how to host and deploy both a frontend React application and a backend .NET Web API onto Microsoft Azure using GitHub Actions.

## Project Structure

The project is split into two independent services:

* **`/Frontend`**: A React application set up using `create-react-app`. It acts as the client-side presentation layer and is configured to bind locally to port `3000`.
* **`/Backend`**: A C# .NET 9 Web API providing REST endpoints (like the default `/weatherforecast`). It is configured to run locally on ports `5000` (HTTP) and `5001` (HTTPS) via `launchSettings.json`.

## Local Development

### Running the Frontend
1. Navigate to the `Frontend` directory:
   ```bash
   cd Frontend
   ```
2. Install dependencies (if not already done):
   ```bash
   npm install
   ```
3. Start the application:
   ```bash
   npm start
   ```
4. Access it in your browser at `http://localhost:3000`.

### Running the Backend
1. Navigate to the `Backend` directory:
   ```bash
   cd Backend
   ```
2. Start the API enforcing the HTTPS profile:
   ```bash
   dotnet run --launch-profile https
   ```
3. Verify the API is running at `https://localhost:5001/weatherforecast`.

## Azure Deployment

This repository utilizes **GitHub Actions** workflows (located in the `.github/workflows` folder) specifically tailored for Azure. These workflows operate independently:

1. **Frontend (Azure Static Web Apps)**
   * Workflow triggers on pushes to the `main` branch.
   * Compiles the React application from the `/Frontend` directory into the `/build` folder and automatically serves it over a globally accessible edge node.

2. **Backend (Azure App Service)**
   * Workflow triggers on pushes to the `main` branch.
   * Compiles the .NET Web API from the `/Backend` directory.
   * Deploys the artifacts to an Azure App Service instance running on a Free (F1) tier.
