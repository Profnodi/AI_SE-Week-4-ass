# Assignment Report — Building Intelligent Software Solutions

Author: Profnodi
Date: 2025-11-23

## 1. Objective & Scope
We built an AI assistant to automate issue classification and triage in software projects. The assistant:
- Classifies issues into labels (bug, feature, docs, question, other).
- Suggests triage actions and priority using model outputs + heuristics.
- Provides code and an optional browser automation demo.

## 2. Theoretical Background (30%)
- Problem framed as supervised text classification.
- Feature engineering: TF-IDF with unigrams + bigrams captures short phrases typical of issues ("null pointer", "UI crash").
- Model: Logistic Regression — robust baseline with calibrated probabilities, interpretable, fast to train.
- Evaluation: accuracy, precision, recall, F1 per class. (See training log/screenshots in appendix.)

## 3. Implementation (50%)
- Data ingestion: GitHub issues CSV or Kaggle dataset.
- Pipeline:
  - clean_text(): lowercase, url removal, punctuation cleaning.
  - vectorization: TfidfVectorizer(max_features=20000, ngram_range=(1,2))
  - classifier: LogisticRegression with simple grid over regularization.
- Files: src/issue_pipeline.py, src/fetch_issues.py, src/predict.py
- Reproducibility: requirements.txt and Colab-ready notebook (notebooks/colab_demo.py).

Screenshots:
- Include screenshots of the model training output and a sample prediction run. (Add when converting to PDF.)

## 4. Ethical Reflection (10%)
Key considerations:
- Data bias: Repositories vary in labeling practices; model inherits biases (over/under-represented labels).
- False positives/negatives: Mislabeling can misroute work; human-in-the-loop is required.
- Privacy: Issue bodies may include sensitive data (logs with secrets). Avoid exposing raw data in shared demos.
- Mitigations:
  - Keep triage suggestions as "recommendations" requiring human approval.
  - Add data filtering to remove PII and secrets, alerting if suspicious tokens appear.
  - Monitor fairness: track label distribution and performance per label; retrain periodically.

## 5. Creativity & Extensions (10%)
Possible extensions:
- Use transformer-based model (DistilBERT) for better understanding of longer bodies.
- Multi-label classification (issues often have multiple labels).
- Integrate with GitHub Actions to auto-comment suggestions on new issues (with a review gate).
- Use active learning to present uncertain cases to maintainers for labeling.

## 6. Deliverables & How to Submit
- Code: Push this repo to GitHub and link it in the submission.
- Report: Convert this report.md to PDF (tools: pandoc or GitHub's render to PDF) and publish as a Community Article.
- Presentation: Follow demo_video_script.md to record a 3-minute video (screen + voice), upload to your course Groups.

Appendix: commands to reproduce
- pip install -r requirements.txt
- python src/fetch_issues.py --owner <owner> --repo <repo> --out data/issues.csv
- python src/issue_pipeline.py --data data/issues.csv --model_out models/issue_clf.joblib
- python src/predict.py --model models/issue_clf.joblib --title "Crash on start" --body "Steps to reproduce..."