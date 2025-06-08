# BodyFat Estimator

A web app to estimate body fat percentage using density and circumference measurements (Siri's equation: Percentage = 495 / Density - 450). Built with Flask, Bootstrap 5.3, and embedded CSS. Deployable to Azure App Service.

## Overview

Estimates body fat for 252 men using underwater weighing and body measurements. Features a modern, responsive UI with input form and result display.

## Features

- Form with placeholders (e.g., Density: 1.0736, Abdomen: 83.6 cm)
- Responsive design with Bootstrap 5.3
- Gradient background, Poppins font
- Info on dataset and Siri's equation
- Result page with "Go Back" button

## Dataset Description

- **Density**: Underwater weighing (gm/cm³)
- **Body Fat**: Siri's equation (Percentage = 495 / Density - 450)
- **Weight**: Pounds (lbs)
- **Abdomen, Chest, Hip**: Circumference (cm)

## Sample data:
|Desity|Abdomen|Chest|Hip|Weight|BodyFat|
|1.0708|85.2|93.1|94.5|154.25|12.3


Source: Dr. A. Garth Fisher, Brigham Young University.

# Installation

```
# Clone the repo
git clone https://github.com/your-username/bodyfat-estimator.git
cd bodyfat-estimator

# Set up virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run locally (Flask)
python app.py
```
## Usage

```
# Open browser to http://localhost:5000
# Enter measurements:
# - Density (e.g., 1.0736)
# - Abdomen (e.g., 83.6 cm)
# - Chest (e.g., 89.2 cm)
# - Weight (e.g., 134.25 lbs)
# - Hip (e.g., 88.8 cm)
# Click "Predict Body Fat"
# View results on show.html, click "Go Back" to retry
```
# Deploying to Azure

```
# Install Azure CLI (if not installed)
# Download from: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

# Log in to Azure
az login
# Select subscription (e.g., Azure subscription 1)

# Register Microsoft.Web provider
az provider register --namespace Microsoft.Web

# Deploy web app (use unique app name, e.g., adiposity-level-estimator)
az webapp up --sku B1 --name adiposity-level-estimator
# Creates App Service Plan, zips and deploys app
# If app exists, updates it

# Verify deployment
# Open URL (e.g., https://adiposity-level-estimator.azurewebsites.net)

# Optional: Set environment variables
az webapp config appsettings set --name adiposity-level-estimator --settings FLASK_APP=app.py

# Optional: Set startup command (for Flask with Gunicorn)
az webapp config set --name adiposity-level-estimator --startup-file "gunicorn app:app"

# Optional: View logs for debugging
az webapp log tail --name adiposity-level-estimator

# Redeploy updates
az webapp up --sku B1 --name adiposity-level-estimator
```

## Notes:
- unique app name (fix typo: adiposity-level-estimator recommended).

- B1 is paid; use F1 for free tier (limited).

- Ensure requirements.txt includes flask, gunicorn, pandas, numpy.

- Add Procfile with web: gunicorn app:app for Azure.

## File Structure
```
bodyfat-estimator/
├── templates/
│   ├── index.html  # Input form
│   └── show.html   # Results page
├── app.py          # Flask backend
├── requirements.txt  # Dependencies
├── Procfile        # Gunicorn config for Azure
├── README.md       # This file
```

## Dependencies

```
# Install dependencies
pip install flask gunicorn pandas numpy

# Generate requirements.txt
pip freeze > requirements.txt
```
- Frontend: Bootstrap 5.3 (CDN), Google Fonts (Poppins)

- Backend: Flask, Gunicorn, Python 3.8+

- Optional: pandas, numpy (for data processing)

