# MLOPs_Assignment4

## Overview
This repository contains the implementation for **Assignment 4** of the MLOps course. The objective is to move from manual execution to automated validation by building and fixing a **GitHub Actions CI pipeline** for an ML project.

## Repository Structure

```
MLOPs_Assignment4/
├── .github/
│   └── workflows/
│       └── ml-pipeline.yml   # GitHub Actions CI pipeline
├── README.md                 # Project documentation
└── requirements.txt          # Python dependencies
```

## GitHub Actions Pipeline

The pipeline is defined in `.github/workflows/ml-pipeline.yml` and runs automatically on every push to any branch **except** `main`.

### Pipeline Steps

| Step | Description |
|------|-------------|
| Checkout Code | Downloads the repository code onto the GitHub runner |
| Set up Python | Installs Python 3.10 on the runner |
| Install Dependencies | Runs `pip install -r requirements.txt` |
| Linter Check | Runs `flake8` to check for syntax and formatting errors |
| Model Dry Test | Verifies PyTorch is installed and working |
| Upload Project Doc | Uploads `README.md` as a GitHub artifact named `project-doc` |

### Trigger Configuration

```yaml
on:
  push:
    branches-ignore:
      - main
  pull_request:
```

## Requirements

All dependencies are listed in `requirements.txt`:

```
torch
flake8
```

## How to Run Locally

1. Clone the repository:
```bash
git clone https://github.com/selsayed2003/MLOPs_Assigment4.git
cd MLOPs_Assigment4
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the linter:
```bash
flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
```

4. Test the model environment:
```bash
python -c "import torch; print('Model environment ready!')"
```

## CI/CD Pipeline

The GitHub Actions pipeline automates all the above steps on every push. To trigger the pipeline, push to any branch other than `main`:

```bash
git checkout -b dev
git push origin dev
```

Then check the **Actions** tab on GitHub to see the pipeline run.
