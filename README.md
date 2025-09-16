# AI Log PoC - Steps Done

Overview

This project is a **Proof of Concept (PoC)** to analyze system logs and detect anomalies. 
The goal is to explore whether AI can help troubleshoot issues faster and identify potential root causes in complex log files, unstructured.

We used sample Hadoop logs to simulate the workflow before considering specific application logs in a test environment.
## What I did so far
Created project folder on my Mac (~/Desktop/AI_Log_PoC).

Used Python 3.12 via Jupyter Notebook, which runs a Python kernel in a browser interface, to write and execute code interactively.

Collected logs:

Downloaded a public, anonymized Hadoop log dataset from LogHub (GitHub).

Loaded logs into a Jupyter Notebook and parsed important fields:

Timestamp (Date + Time)

Log level (INFO, WARN, ERROR)

Thread / Process

Component

Message / Event

Phase 1: Initial anomaly detection

Explored the logs and identified patterns manually.

Phase 2: AI-assisted anomaly detection

Converted timestamps to numeric values.

Encoded log levels numerically.

Ran Isolation Forest to detect anomalies in logs.

Previewed top anomalous entries and visualized results with charts.

Confirmed proof of concept: AI can help find unusual log events.

Initialized Git repository locally and pushed all files to GitHub.

Created a README to document steps, safety checks, and next actions.

**Phase 1: Setup and GitHub**

## Log Data Used
Hadoop logs from LogHub were used as a substitute for the target application logs to safely test the AI log analysis workflow. They have a similar structure with timestamps, log levels, components, and messages with the target application that needs proof of Concept validated. This allows us to practice parsing, anomaly detection, and visualization before working with real application logs in a test environement.

## Next Steps
- Improve anomaly detection with **template rarity** (rare log patterns).  
- Add more **features** for machine learning (capital words, message length, special characters).  
- Generate **better visualizations** of anomalies.  
- Use this project as example and foundational work for replicating the process in a possible test environement to handle **specific application logs** when they become available.

**Phase 2: Anomaly Detection**

In this phase, the PoC applies AI-based anomaly detection on structured Hadoop sample logs. Using a machine learning model (Isolation Forest), the notebook identifies unusual log events, including errors and unexpected behaviors. The model successfully flagged the top anomalies and visualized them over time, demonstrating that AI can help highlight potential root causes in log data. This confirms the feasibility of using AI to assist in log analysis and troubleshooting, forming a solid proof of concept for future work with live application logs.

## Phase 3: Correlation + Visualization

- Filtered only anomalies from Phase 2.  
- Summarized top error messages from anomalous logs.  
- Visualized anomalies on a timeline to show patterns over time.
  
**Results / Proof of Concept**

Top anomalies detected: Errors from RMCommunicator Allocator in Hadoop logs.

Visualization: Shows unusual log events over time.

Conclusion: AI successfully identifies anomalous log entries, confirming the feasibility of using AI to assist in log analysis and troubleshooting.

The PoC shows anomaly detection works in principle, is a work in progress so far latest phase prooved it can:

- Successfully highlight correlations and patterns in anomalies.  
- Provide insight into error trends and potential root causes.  
- PoC confirmed that anomaly detection works in principle and can support troubleshooting.

  **Next step** is to test on other dataset and unstructured data, ongoing checks are to find best substitutes

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

git pull origin main --rebase → Updates your local branch with remote changes

git push -u origin main → uploads files to GitHub

🔹 Jupyter / Python Commands

These commands were used to read and test the Hadoop sample logs.
They only worked on the local file and did not change the logs themselves.
All plotting and processig was done locally.

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

import pandas as pd
Loads the pandas library for data manipulation. 

import numpy as np
Loads numpy for numeric computations. 

from sklearn.ensemble import IsolationForest
Imports the machine learning model used for anomaly detection. Safe.

import matplotlib.pyplot as plt
Loads matplotlib for visualizing anomalies. 

logs = pd.read_csv("loghub/Hadoop/Hadoop_2k.log_structured.csv")
Reads structured log file into memory. Read-only. 

logs['timestamp'] = pd.to_datetime(logs['Date'] + ' ' + logs['Time'])
Combines Date + Time columns into a datetime object.

logs['timestamp_num'] = logs['timestamp'].astype(int) / 10**9
Converts datetime to seconds since epoch. 

level_map = {'INFO': 0, 'WARN': 1, 'ERROR': 2}
logs['level_num'] = logs['Level'].map(level_map)
Converts log levels to numeric for ML analysis. 

model = IsolationForest(contamination=0.05, random_state=42)
Initializes the anomaly detection model.

logs['anomaly'] = model.fit_predict(logs[['timestamp_num', 'level_num']])
Runs anomaly detection. Adds a new column with predictions. Safe; non-destructive.

logs[logs['anomaly'] == -1].head(10)
Displays the top 10 anomalous log entries; read-only.

plt.scatter(...)
Generates visualizations for anomalies; only plots data.
anomalies = logs[logs['anomaly'] == -1]

Filters only anomalous log entries from your dataset.

Operates locally on the DataFrame; no external access.

error_summary = anomalies['Content'].value_counts().head(10)

Counts the 10 most frequent error messages among anomalies.

Local computation; no sensitive info exposed.

plt.scatter(...) and plt.figure(...)

Visualizes anomalies on a timeline.

Only displays data you already have locally.

anomaly_counts = anomalies.set_index('timestamp').resample('1min').size()

Aggregates anomalies per minute for frequency analysis.

Local processing; no external connections.

anomaly_counts.plot(kind='bar', ...)

Plots anomaly frequency as a bar chart.

Visualization only; local operation.

👉 Note:

All Git commands just handle saving and uploading the project.

All Python commands only read and analyze the local CSV log file.

No external systems, no sensitive data touched.

x
