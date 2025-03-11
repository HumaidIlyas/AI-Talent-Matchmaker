# AI-Talent-Matchmaker
Automated matchmaking for like-minded professionals using semi-supervised learning. Scored users based on role, company, education &amp; skills to enable meaningful connections.

## **Overview**
At **CoffeeMug.AI**, a professional matchmaking startup, I was responsible for automating the **manual scoring system** used to match professionals based on multiple attributes. 

Initially, human experts assigned scores based on:
- **Company Name**
- **Role & Experience**
- **Industry**
- **University/Education**
- **Skills**

Since the labeled dataset **grew rapidly**, automation became necessary to ensure scalability and efficiency. To achieve this, I developed a **semi-supervised learning pipeline** that could infer scores similar to human judgment.

---

## **Challenges & Data Preprocessing**
The manual scoring relied on a **complex system of weights**, which human annotators used implicitly. These weights were stored in **master tables**, which contained:

1. **Industry Weights:** Assigning scores based on the industry the professional belongs to.
2. **Premium Education:** Identifying **elite universities** (IITs, IIMs, Ivy Leagues, etc.).
3. **Role Weights:** Different job titles had varying impacts (e.g., a **Senior Data Scientist** vs. a **Junior Data Scientist**).
4. **Company Weights:** Some companies had higher weightage (e.g., working at **Google** vs. a startup).
5. **Composite Weighting:**  
   - A **high role at a small company** could be similar to a **low role at a big company**.
   - This meant **role and company scores** were interdependent.

### **1 Data Extraction & Cleaning**
- Extracted structured data from **LinkedIn profiles** using JSON parsing.
- Filtered relevant sections:
  - **Work Experience**: Start/End Dates, Job Title, Company Name.
  - **Education**: University, Degree, Field of Study.
  - **Skills**: Extracted and matched against the **industry skills master list**.
- Cleaned company names and standardized different spellings (e.g., "Google LLC" vs. "Google Inc.").

### **2 Master Table Mapping**
- Mapped professionals’ attributes to the **predefined master tables**.
- Assigned weights based on:
  - **Education (Elite vs. Non-Elite)**
  - **Company Reputation**
  - **Industry Importance**
  - **Job Title Significance**
- Created **lookup functions** to dynamically assign weights.

### **3 Feature Engineering**
- **Experience Calculation:** Used the **earliest job start date** to estimate **total work experience**.
- **Role-Company Combination:** Generated a **weighted score** that accounted for:
  - **Company prestige**
  - **Seniority level in the company**
- **Industry Normalization:** Converted industry categories into numeric representations.

### **4 Semi-Supervised Learning Approach**
Since we had a growing **hand-labeled dataset**, a **semi-supervised learning approach** was adopted:
- **Labeled Data:** Used the manually scored dataset for supervised learning.
- **Unlabeled Data:** Assigned **pseudo-labels** using an iterative **self-training** method.
- **Model Selection:**
  - Explored **XGBoost, Random Forest, and Logistic Regression**.
  - Chose **XGBoost** due to its ability to handle missing data and categorical interactions.
- **Active Learning:** Periodically **retrained the model** as new manual scores were added.

### **5 Model Deployment & Automation**
- The trained model was integrated into **CoffeeMug.AI’s platform**.
- It **automatically generated scores** for new professionals.
- **Batch scoring** was implemented for **daily updates**.
- **Logging & Feedback Loop:**  
  - Monitored predictions to detect inconsistencies.
  - Allowed human reviewers to fine-tune difficult cases.

---

## **Results & Impact**
- **Reduced manual effort** in scoring new professionals.  
- **Improved consistency** by aligning AI predictions with human judgment.  
- **Enabled scalability**—professionals could be **scored in real-time**.  
- **Adaptive Learning**—the model improved with **new labeled data** over time.  

---

## **Note**
⚠️ I cannot share the code files due to confidentiality, but this document outlines the **thought process, data handling, and techniques used**.

---
