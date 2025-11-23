# Building Intelligent Software Solutions — Assignment

This repository contains a complete submission for the course assignment "Building Intelligent Software Solutions". It includes:

- A reproducible AI implementation (issue classifier + triage assistant).
- Training and inference scripts, plus a Colab-friendly notebook.
- A report (convertible to PDF) with theory, screenshots, and ethical reflection.
- A 3-minute demo script and instructions to record/share the video.

High-level idea
- Use AI to automate software-engineering tasks: classify GitHub issues (bug/feature/docs/etc.) and suggest triage actions (labels, priority, assignee hints).
- Implementation uses: Pandas, Scikit-learn (TF-IDF + Logistic Regression), optional Selenium automation for demoing issue filing/triage.

How to run (quick)
1. Create a Python 3.9+ venv and install:
   pip install -r requirements.txt
2. Prepare data:
   - Option A: Download a Kaggle GitHub issues dataset (instructions below).
   - Option B: Use your repository's issues via `GITHUB_TOKEN` (see src/fetch_issues.py).
3. Train:
   python src/train.py --data data/issues.csv --model models/issue_clf.joblib
4. Predict:
   python src/predict.py --model models/issue_clf.joblib --text "App crashes when clicking Save"

Files of interest
- src/train.py : training pipeline
- src/predict.py : single-sentence inference
- src/fetch_issues.py : helper to fetch issues from GitHub (uses token)
- notebooks/colab_demo.py : Colab-ready step-by-step notebook (python script with cells)
- report.md : report content to convert to PDF
- demo_video_script.md : 3-minute demo outline and talking points

Academic integrity
- Use this repo as your submission. Cite any external datasets (Kaggle, GitHub).
- Ethical reflection included in the report.

Contact
- Author: Profnodi (student). Use the repo's Issues for questions.