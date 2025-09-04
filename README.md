# AI Log PoC - Steps Done

This project is a **Proof of Concept (PoC)** to test AI-based log analysis. The goal is to explore how we can detect unusual log entries automatically, which can later be applied to Genesys application logs.

## Log Data Used
Hadoop logs from LogHub were used as a substitute for Genesys logs to safely test the AI log analysis workflow. They have a similar structure with timestamps, log levels, components, and messages. This allows us to practice parsing, anomaly detection, and visualization before working with real Genesys logs.

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
- Use this project as example and foundational work for replicating the process in a possible test environement to handle **Genesys logs** when they become available.

x
