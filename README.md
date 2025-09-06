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

All commands and code used in this PoC are purely analytical and do not execute any log data as code or connect to external endpoints (except GitHub for repository storage). 

🔹 Git / GitHub Commands

These commands were used to set up version control and upload the project to GitHub.
They only affect the project folder, nothing else.

git init → starts Git tracking in the folder

git add . → marks files to be included in the next commit

git commit -m "message" → saves a snapshot of changes locally

git branch -M main → renames the branch to main

git remote add origin <URL> → connects the project to GitHub

git push -u origin main → uploads files to GitHub

🔹 Jupyter / Python Commands

These commands were used to read and test the Hadoop sample logs.
They only worked on the local file and did not change the logs themselves.

Importing libraries

import pandas as pd → loads the Pandas library for data handling

from sklearn.ensemble import IsolationForest → loads the anomaly detection model

Reading the log file

pd.read_csv("Hadoop_2k.log_structured.csv") → opens the log file

logs.head() → shows the first rows of data

Formatting and exploring

pd.to_datetime(...) → converts timestamps into date format

logs.describe() → quick summary (counts, averages, etc.)

Running anomaly detection

IsolationForest(...) → sets up the anomaly detection model

model.fit(...) → trains the model on selected columns

model.predict(...) → adds a column marking “normal” vs “anomaly”

logs[logs['anomaly'] == -1] → shows only anomalies

👉 Note:

All Git commands just handle saving and uploading the project.

All Python commands only read and analyze the local CSV log file.

No external systems, no sensitive data touched.

x
