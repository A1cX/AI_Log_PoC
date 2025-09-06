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

These are the commands I used to set up version control and share my project on GitHub:

git init	Starts a new Git repo in the folder	Just sets up tracking for changes
git add .	Selects all files to be included in the next commit	Doesn’t change the files, just marks them
git commit -m "message"	Saves a snapshot of your changes	Safe, only local
git branch -M main	Renames the default branch to main	A naming step, nothing more
git remote add origin <URL>	Connects your local repo to GitHub	Only sets the link to GitHub
git push -u origin main	Uploads the project to GitHub	Sends files you chose to your repo

Jupyter / Python Commands:

These commands were used to open, look at, and run a simple anomaly detection test on logs.
They only work with the local CSV file, and don’t execute or change the logs themselves.

import pandas as pd	Loads Pandas library for data handling	Standard setup step
logs = pd.read_csv("Hadoop_2k.log_structured.csv")	Opens the log file into memory	Only reads the file
logs.head()	Shows the first rows	For preview only
logs['timestamp'] = pd.to_datetime(logs['timestamp'])	Converts timestamps into date/time format	Just formatting
logs.describe()	Gives a quick summary (counts, averages, etc.)	Read-only
from sklearn.ensemble import IsolationForest	Loads the anomaly detection model	Library import
model = IsolationForest(contamination=0.01, random_state=42)	Sets up the anomaly detection model	Safe initialization
model.fit(logs[['feature1','feature2']])	Trains the model on chosen data columns	Works only on numbers in the log
logs['anomaly'] = model.predict(logs[['feature1','feature2']])	Marks rows as “normal” or “anomaly”	Adds a column
logs[logs['anomaly'] == -1]	Shows only the anomalies	Read-only view

To sum it up:
👉 Git commands just handle saving and uploading.
👉 Python commands just read, format, and analyze the test log file.

x
