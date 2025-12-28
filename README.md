# Insurance Data Engineering Pipeline: Oracle to CSV via IICS

## 📌 Project Overview
This project demonstrates an end-to-end Data Integration (ETL) pipeline designed for the insurance industry. Using **Informatica Intelligent Cloud Services (IICS)** and **Oracle SQL**, I built a solution that automates data cleansing, detects high-risk fraudulent claims, and generates  Payment Analytics .

<img width="948" height="276" alt="🛠 Tech Stack - visual selection" src="https://github.com/user-attachments/assets/07b77998-89e1-4873-9000-cccb33365791" />


## 🛠 Tech Stack
* **Source Database:** Oracle 19c (Relational)
* **ETL Tool:** Informatica Intelligent Cloud Services (IICS) - Cloud Data Integration
* **Orchestration:** IICS Taskflows
* **Target:** Flat Files (CSV/Excel compatible)

## 🚀 Business Use Cases & Logic

### 1. Data Hygiene 
* **Problem:** Legacy systems often produce records with missing IDs or invalid age entries.
* **Logic:** Implemented a validation gate using IICS Filter and Expression transformations.
* **Output:** Valid records are processed; anomalies are routed to `TGT_wrong_customer.csv` for the Data Quality team.

<img width="1686" height="796" alt="image" src="https://github.com/user-attachments/assets/977a8b6f-2129-48c9-8d43-4c9c1a96bd5d" />



### 2. Fraud Detection 
* **Problem:** Claims filed within 30 days of policy inception are high-risk for fraud.
* **Logic:** Performed a **Joiner** between `POLICY` and `CLAIM` tables. Used a Date Transformation to calculate the window.
* **Output:** High-risk records are flagged and exported to `TGT_Early_claim_Detection.csv`.

   <img width="1677" height="822" alt="image" src="https://github.com/user-attachments/assets/d9194092-74c6-41c1-b95e-b8899d80b2bc" />



### 3. Multi-Target Payment Analytics 
* **Problem:** The Finance department needs two separate streams of data: one for the Collections team to follow up on overdue accounts, and one for the Accounting team to track successful revenue..
* **Logic:** Built a 3-way join between CUSTOMER, POLICY, and PAYMENT tables. Using a Router Transformation (or separate Filter paths), I segmented the data based on the PAYMENT_STATUS field.
* **Output:** A clean CSV report (`TGT_Pending.csv`) delivered to the Finance team.

   <img width="1666" height="817" alt="image" src="https://github.com/user-attachments/assets/50341d38-d354-42ac-ab9f-e0d5aed1e90f" />



## ⛓ Orchestration 
I designed a **Taskflow** to automate the execution. 
1. It begins with the **Customer Cleaning** task.
2. Upon success, it runs the **Fraud Detection** and **Delinquency Reporting** tasks in parallel to optimize performance.

 <img width="1656" height="822" alt="image" src="https://github.com/user-attachments/assets/1280e7dd-c818-458c-ae8f-df5d6ecf4ae1" />


