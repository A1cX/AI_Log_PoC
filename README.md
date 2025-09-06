# AI Log PoC - Steps Done

This project is a **Proof of Concept (PoC)** to test AI-based log analysis. The goal is to explore how we can detect unusual log entries automatically, which can later be applied to a specific application logs.

## Log Data Used
Hadoop logs from LogHub were used as a substitute for Genesys logs to safely test the AI log analysis workflow. They have a similar structure with timestamps, log levels, components, and messages with the target application that needs proof of Concept validated. This allows us to practice parsing, anomaly detection, and visualization before working with real application logs in a test environement.

## What I did so far
1. **Created project folder** on my Mac (`~/Desktop/AI_Log_PoC`).  
2. **Installed Python 3.12** and Jupyter Notebook to run code.  
3. **Collected logs**:  
   - Copied Mac system logs for practice.  
   - Downloaded a public, anonymized Hadoop log dataset from LogHub (GitHub).  
4. **Loaded logs into a notebook** and parsed important fields:  
   - Timestamp  
   - Log level (INFO, WARN, ERROR)  
   - Thread  
   - Component  
   - Message  
5. **Ran basic anomaly detection** using Python (Isolation Forest) to find unusual log entries.  
6. **Visualized results** with simple tables and charts.  
7. **Initialized Git repository** locally and pushed all files to GitHub.  
8. **Created a README** to document steps and next actions.  

## Next Steps
- Improve anomaly detection with **template rarity** (rare log patterns).  
- Add more **features** for machine learning (capital words, message length, special characters).  
- Generate **better visualizations** of anomalies.  
- Use this project as example and foundational work for replicating the process in a possible test environement to handle **specific application logs** when they become available.
## Safety Notes

All commands and code used in this PoC are purely analytical and do not execute any log data as code or connect to external endpoints (except GitHub for repository storage). The table below summarizes each step and its purpose.

Step / Command and Purpose
Safety / Notes
cd ~/Desktop/AI_Log_PoC
Move into project folder
- local folder navigation only
git init
Initialize local Git repository
- sets up Git tracking
git add .
Stage all files for commit
- no code execution
git commit -m "message"
Commit files locally
- records snapshot of files
git remote set-url origin https://...
Set remote GitHub repository
– configuration only
git push -u origin main
Upload commits to GitHub
- uploads files, no code execution
ls / pwd / mv loghub-master loghub
List, show path, rename folder
– local file operations
import pandas as pd
Load Python library for data
- standard library import
logs = pd.read_csv("Hadoop_2k.log_structured.csv")
Load log CSV into DataFrame
- reads local file only
logs['timestamp'] = pd.to_datetime(logs['timestamp'])
Convert timestamp column
 – data transformation
from sklearn.ensemble import IsolationForest
Import anomaly detection model
- library import
model = IsolationForest(contamination=0.01)
Initialize anomaly detection
– local computation
model.fit(logs[['feature1','feature2']])
Train model on selected features
- works on local data only
logs['anomaly'] = model.predict(logs[['feature1','feature2']])
Mark anomalies
- no external access
logs[logs['anomaly'] == -1]
Filter detected anomalies
- local data filtering

x
