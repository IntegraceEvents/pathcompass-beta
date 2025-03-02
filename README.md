# **PATH Compass - Course recommender**

**Version:** 1.0  
**Author:** Edinburgh Elephants  
**Status:** Beta (Prototype)  
**License:** MIT  

<img width="1440" alt="image" src="https://github.com/user-attachments/assets/50d0a454-db33-4a8b-bf16-a8742796bf2a" />


---

## **Overview**  
PATH Compass is a prototype course match calculator designed to help users compare and select university courses based on their preferences. Users can specify their preferences in natural language or manually adjust various parameters such as pass rate, assessment structure, instructor rating, popularity, and topics of interest. The system calculates a match score for each course using an algorithm and ranks them accordingly. In the future, the system can be easily modified to accept interest from prospective students to help them choose an appropriate degree with an university easily.

---
## **Backstory: Why we created PATH Compass**  

As a new students, we often found it **difficult to choose courses** that matched our interests, workload preferences, and strengths. University course descriptions can be **vague**, and official databases don’t provide easy ways to **compare** courses based on individual priorities.  

When discussing this with peers, we realised that **many students faced the same issue**—spending hours **researching courses**, manually comparing assessment structures, pass rates, and instructor ratings.  

At the same time, our **interest in AI and automation** made us wonder:  
**What if we could build a tool that helps students find their ideal courses effortlessly?**  

Thus, **PATH Compass** was created by us during the HackTheBurgh – app, that lets students input their preferences in **plain language** and/or manually tweak settings, and then **automatically finds the best-matching courses**.

---

## **Development process: how we built it**  

### **1. Planning & Research**  
- We first identified **key factors students care about** when choosing courses (e.g., **pass rate, instructor rating, assessment structure, topics of interest, popularity**).  
- We reviewed **existing and provided to us course databases** (like DRPS at the University of Edinburgh) and realized that there’s **no structured way to compare courses easily**.  

### **2. Choosing technologies**  
To build PATH Compass, we used:  
- **Frontend:** HTML, CSS, JavaScript (Just for demo purposes. In a realistic scenario, backend would be implemented with server-side processing)  
- **Data processing:** JavaScript & **PapaParse.js** (for CSV handling)  
- **AI features:** Google **Gemini Flash API** (for natural language processing & explanations)  
- **Data storage:** A **static CSV file** (as a placeholder for a real database or API)  

### **3. Algorithm development**  
We created a **scoring algorithm** to rank courses based on user preferences:  
- **Normalized values** are computed for parameters like **pass rate, instructor rating, and assessment distribution**.  
- **Weighted scoring** assigns different importance levels to each parameter.  
- **Topics of interest matching** uses **Jaccard similarity** to allow **partial matches** (e.g., “Software Engineering” partially matching “Software Security”).  

### **4. Implementing AI for natural language input**  
- We integrated **Google Gemini AI** to convert **plain English input** into structured parameters.  
- Example: If a user types *"I prefer easy courses with high pass rates and fewer assessments"*, the AI extracts:  
  ```json
  {
    "pass_rate": "High",
    "num_assessments": 3,
    "care_pass_rate": 100,
    "care_num_assessments": 100
  }
  ```
- This makes the tool **more user-friendly** for students who don’t want to manually adjust sliders and inputs.  

### **5. Implementing "Ask AI" feature**  
- We added a feature where users can **ask questions about a course using Gemini AI** by using special button under each course tab.  
- This fetches course information from the **DRPS website**, but due to **CORS restrictions**, users must install a **CORS extension** (this would be solved in a real deployment using **Node.js as a proxy**).  

### **6. Testing & iteration**  
- We tested with **synthetic data** (fake) to adjust **matching accuracy**.  
- Adjusted **weighting mechanisms** to prevent bias towards certain parameters.  
- Iterated on **UI improvements** to make the interface more intuitive ans simple for the prospective user.  

---

## **Technical Overview**  
1. **User inputs preferences:**  
   - They can either type a **natural language request** or manually adjust parameters.  

2. **Data processing & matching algorithm:**  
   - The system **loads course data from a CSV file** (in a real deployment, this would be replaced by a **live university API**).  
   - Each course is assigned a **match score (0-100%)** based on the **user’s preferences** and **normalized values**.  

3. **Scoring breakdown:**  
   - **Pass Rate, Instructor Rating, Assessment Structure, Popularity** → **Normalized & Weighted**  
   - **Topics of interest matching** → **Jaccard similarity calculation**  
   - The final **match score** is computed with a formula:  
    <img width="167" alt="image" src="https://github.com/user-attachments/assets/3bdc9232-88c4-451e-a0fe-21d717fa8c85" />


4. **AI enhancements:**  
   - **Gemini AI extracts preferences** from natural language input.  
   - **Gemini AI provides reasoning** on why a course is a good match.  
   - **"Ask AI" fetches external course details** and answers user queries.  

5. **Results displayed:**  
   - Courses are **ranked by match score**.  
   - Users can view **detailed explanations** and ask additional questions.  

---

## **Features**  

### **1. Smart preference setter (AI-powered input processing)**
- Users can describe their ideal course in natural language, and the system extracts structured preferences using **Google Gemini Flash**.
- Automatically assigns importance weightings (0-100%) to relevant parameters.
- Supports auto-filling for pass rate, assessment ratio, number of assessments, instructor rating, popularity, and topics of interest.

### **2. Customizable Course Matching Parameters**
- Users can manually adjust:
  - Pass rate (Low, Medium, High)
  - Assessment distribution (Exam, Individual, Group)
  - Number of assessments
  - Instructor rating threshold
  - Topics of Interest (manual tag input)
  - Popularity level (Low, Medium, High)
  - Gender distribution

### **3. Real-time Match Score Calculation**
- The system assigns a match percentage based on **user preferences and course attributes**.
- Supports partial matches for **Topics of Interest**, computing similarity using a **Jaccard-based approach**.
- Generates a ranked list of courses based on scores.

### **4. Course Details & Reasoning Explanation**
- Each course has a **detailed breakdown** of attributes.
- Users can request a **human-friendly explanation** (via Gemini AI) on why a course is a good match.

### **5. "Ask About Course" Feature**
- Users can **ask questions** about a course.
- The system retrieves **course details** and fetches data from an official course website.
- Answers are generated via Gemini AI.

---

## **Algorithm for match score calculation**  

Each course receives a **match score (0-100%)**, calculated as follows:

### **1. Parameter normalization**
Each numeric value is normalized between 0 and 1 using:<br>
<img width="318" alt="image" src="https://github.com/user-attachments/assets/9b56a3aa-8a6d-47ec-929b-08868a51076f" />


### **2. Parameter score calculation**
Each parameter contributes to the total score. The formula for each parameter’s contribution:

<img width="502" alt="image" src="https://github.com/user-attachments/assets/c29394c3-877b-4b23-9094-718bd637454d" />

### **3. Topics of interest matching (Jaccard Similarity)**
For **Topics of interest**, partial matching is computed using **word-based Jaccard similarity**:

<img width="238" alt="image" src="https://github.com/user-attachments/assets/2c858b2c-14ac-47ff-b63b-45a8184adca7" />


Where:  
<img width="230" alt="image" src="https://github.com/user-attachments/assets/ca95f615-cdde-4a83-9f93-197e9249e4b7" />


Example:  
User input: **"Software Engineering"**  
Course tag: **"Software Security"**  
<img width="95" alt="image" src="https://github.com/user-attachments/assets/eb7642b3-2a55-41c2-a9a3-302a40424b49" />


If at least **one word matches**, the score is partially credited.

### **4. Final match score**
The final match score is calculated as the weighted sum of all parameter scores:

<img width="250" alt="image" src="https://github.com/user-attachments/assets/ead36b69-9444-42d9-a070-a7966d12e38c" />


---

## **Future improvements**
1. **Synthetic dataset**  
   - The current dataset is **not real** and cannot be currently used by **University of Edinburgh (UoE) students**.
   - In a real scenario, data would need to come from **UoE’s official API**.

2. **AI not implemented in decision-making**  
   - The **matching algorithm is purely rule-based**.
   - AI **does not** influence the scoring process.
   - **Topics of Interest matching is non-AI-based**, meaning:
     - **"Software Engineering" ≠ "Web Development"**
     - Only **word overlap** is considered.

3. **Static CSV database**  
   - Course data is **loaded from a static CSV file**.
   - In a real-world system, an **API should be used** to update courses **daily**.

4. **CORS violation in "Ask AI" feature**  
   - The **"Ask AI"** feature fetches course details from the **DRPS website**, which is on a different domain.  
   - Browsers block these requests due to **CORS policies**, requiring users to install a **CORS extension** (e.g., **Allow CORS** for Chrome).  
   - In a **real-world scenario**, this could be resolved by using a **server-side proxy** (e.g., **Node.js with Express**) to handle requests securely.

---

## **Installation requirements**

To use the **"Ask"** feature, which fetches course details from the **DRPS website**, you need to bypass **CORS restrictions** since the DRPS page is on a different domain.  

### **Solution: install a CORS Extension**  
1. **For Chrome:** Install [Allow CORS: Access-Control-Allow-Origin](https://chromewebstore.google.com/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf?hl=en)  
2. **For Firefox:** Install [CORS Everywhere](https://addons.mozilla.org/en-US/firefox/addon/cors-everywhere/)  

After installation, **enable the extension** before using the "Ask AI" feature.

---

## **Contributors – team Edinburgh Elephants:**
- Shlok Gupta  
- Matvii Yatsenko  
- Yufeng Xia  
- Danylo Khrystenko  
- Daniel Hornung  

---

## **References**  
- [GeeksforGeeks](https://www.geeksforgeeks.org/)  
- [W3Schools](https://www.w3schools.com/)  
- [ChatGPT](https://chatgpt.com/)  
- [Gemini API](https://ai.google.dev/)  

