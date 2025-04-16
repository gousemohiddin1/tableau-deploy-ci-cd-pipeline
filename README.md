# 📊 Tableau CI/CD Pipeline (GitHub Actions)

This repository demonstrates a CI/CD workflow for publishing Tableau workbooks (`.twb` / `.twbx`) to Tableau Server or Tableau Cloud using **GitHub Actions** and **Python** (`tableauserverclient`).

---

## ✅ Features

- Automatically publishes Tableau dashboards when code is pushed to specific branches (e.g., `main`, `stage`)
- Supports multiple environments with branch-based logic
- Secure deployment using GitHub Secrets
- Publishes `.twb` / `.twbx` workbooks via custom Python script

---

## 🧰 Tech Stack

- GitHub Actions
- Python 3.10+
- Tableau Server Client (`tableauserverclient`)
- Tableau Server or Tableau Cloud

---

## 📁 Folder Structure

```
.
├── .github/
│   └── workflows/
│       └── tableau-deploy.yml        # CI/CD workflow
├── publish_to_tableau.py             # Python script to publish dashboards
├── dashboards/
│   └── my_dashboard.twbx             # Tableau workbook
├── README.md
```

---

## 🔧 GitHub Secrets to Configure

| Secret Name           | Description                                  |
|-----------------------|----------------------------------------------|
| `TABLEAU_USERNAME`    | Tableau username used to publish             |
| `TABLEAU_PASSWORD`    | Tableau password or personal access token    |
| `TABLEAU_SITE_ID`     | Site ID (use empty string `""` if default)   |
| `TABLEAU_PROJECT`     | Target project name in Tableau               |
| `TABLEAU_SERVER_URL`  | Tableau Server or Tableau Cloud URL          |

---

## 🚀 How the Pipeline Works

### 1. Developer pushes a change (e.g., new `.twb` file) to the `main` or `stage` branch  
### 2. GitHub Actions triggers the `tableau-deploy.yml` workflow  
### 3. The `publish_to_tableau.py` script is executed with credentials from GitHub Secrets  
### 4. Tableau workbook is published to the appropriate project and site  

---

## 🛠️ Setup Instructions

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-username/tableau-ci-cd-pipeline.git
cd tableau-ci-cd-pipeline
```

### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```
> Or just: `pip install tableauserverclient`

### Step 3: Create GitHub Secrets  
Go to your repo → **Settings → Secrets → Actions** → **New repository secret**  
Add all required secrets listed above.

### Step 4: Update Python Script (Optional)  
Edit `publish_to_tableau.py` to reflect:  
- Your file path  
- Project name (optional if using secret)  
- Site ID or token auth  

### Step 5: Push to GitHub  
When you push to the `main` or `stage` branch, your Tableau workbook will be deployed automatically.

---

## 📄 Example GitHub Workflow (`tableau-deploy.yml`)

```yaml
name: Deploy Tableau Workbook

on:
  push:
    branches:
      - main
      - stage

jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      TABLEAU_USERNAME: ${{ secrets.TABLEAU_USERNAME }}
      TABLEAU_PASSWORD: ${{ secrets.TABLEAU_PASSWORD }}
      TABLEAU_SITE_ID: ${{ secrets.TABLEAU_SITE_ID }}
      TABLEAU_PROJECT: ${{ secrets.TABLEAU_PROJECT }}
      TABLEAU_SERVER_URL: ${{ secrets.TABLEAU_SERVER_URL }}

    steps:
      - name: Checkout repo
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: pip install tableauserverclient

      - name: Deploy to Tableau
        run: python publish_to_tableau.py
```

---

## 👨‍💻 Author

**Gouse Mohiddin Sheik**  
BI Architect | Tableau | Power BI | Snowflake  
[LinkedIn](https://www.linkedin.com/in/gouse-mohiddin-sheik-92425236/)

---

## 📜 License

MIT License
