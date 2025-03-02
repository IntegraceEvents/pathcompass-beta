# **PATH Compass - Course Recommender**

**Version:** 1.0  
**Author:** Edinburgh Elephants  
**Status:** Beta (Prototype)  
**License:** MIT  

---

## **Overview**  
PATH Compass is a prototype course match calculator designed to help users compare and select university courses based on their preferences. Users can specify their preferences in natural language or manually adjust various parameters such as pass rate, assessment structure, instructor rating, popularity, and topics of interest. The system calculates a match score for each course using an algorithm and ranks them accordingly.

---
## **Backstory: Why We Created PATH Compass**  

As students, we often found it **difficult to choose courses** that matched our interests, workload preferences, and strengths. University course descriptions can be **vague**, and official databases don’t provide easy ways to **compare** courses based on individual priorities.  

When discussing this with peers, we realized that **many students faced the same issue**—spending hours **researching courses**, manually comparing assessment structures, pass rates, and instructor ratings.  

At the same time, our **interest in AI and automation** made us wonder:  
**What if we could build a tool that helps students find their ideal courses effortlessly?**  

Thus, **PATH Compass** was born—a tool that lets students input their preferences in **plain language** or manually tweak settings, and then **automatically finds the best-matching courses**.

---

## **Development Process: How We Built It**  

### **1. Planning & Research**  
- We first identified **key factors students care about** when choosing courses (e.g., **pass rate, instructor rating, assessment structure, topics of interest, popularity**).  
- We reviewed **existing course databases** (like DRPS at the University of Edinburgh) and realized that there’s **no structured way to compare courses easily**.  

### **2. Choosing Technologies**  
To build PATH Compass, we used:  
- **Frontend:** HTML, CSS, JavaScript (Just for demo purposes. In a realisitc scenario, backend would be implemented with server-side processing)  
- **Data Processing:** JavaScript & **PapaParse.js** (for CSV handling)  
- **AI Features:** Google **Gemini Flash API** (for natural language processing & explanations)  
- **Data Storage:** A **static CSV file** (as a placeholder for a real database or API)  

### **3. Algorithm Development**  
We created a **scoring algorithm** to rank courses based on user preferences:  
- **Normalized values** are computed for parameters like **pass rate, instructor rating, and assessment distribution**.  
- **Weighted scoring** assigns different importance levels to each parameter.  
- **Topics of Interest Matching** uses **Jaccard similarity** to allow **partial matches** (e.g., “Software Engineering” partially matching “Software Security”).  

### **4. Implementing AI for Natural Language Input**  
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

### **5. Implementing "Ask AI" Feature**  
- We added a feature where users can **ask questions about a course**.  
- This fetches course information from the **DRPS website**, but due to **CORS restrictions**, users must install a **CORS extension** (this would be solved in a real deployment using **Node.js as a proxy**).  
- AI generates **concise, human-friendly answers** based on course data.  

### **6. Testing & Iteration**  
- We tested with **synthetic data** to fine-tune **matching accuracy**.  
- Adjusted **weighting mechanisms** to prevent bias towards certain parameters.  
- Iterated on **UI improvements** to make the interface more intuitive.  

---

## **How PATH Compass Works (Technical Overview)**  
1. **User Inputs Preferences:**  
   - They can either type a **natural language request** or manually adjust parameters.  

2. **Data Processing & Matching Algorithm:**  
   - The system **loads course data from a CSV file** (in a real deployment, this would be replaced by a **live university API**).  
   - Each course is assigned a **match score (0-100%)** based on the **user’s preferences** and **normalized values**.  

3. **Scoring Breakdown:**  
   - **Pass Rate, Instructor Rating, Assessment Structure, Popularity** → **Normalized & Weighted**  
   - **Topics of Interest Matching** → **Jaccard Similarity Calculation**  
   - The final **match score** is computed as:  
     \[
     \text{Final Score} = \sum_{i=1}^{n} (\text{Parameter Score}_i)
     \]

4. **AI Enhancements:**  
   - **Gemini AI extracts preferences** from natural language input.  
   - **Gemini AI provides reasoning** on why a course is a good match.  
   - **"Ask AI" fetches external course details** and answers user queries.  

5. **Results Displayed:**  
   - Courses are **ranked by match score**.  
   - Users can view **detailed explanations** and ask additional questions.  

---

## **Future Improvements**  
- **Switch from static CSV to a live API** for real-time course updates.  
- **Use AI embeddings (e.g., Word2Vec, BERT)** for **better topic matching**.  
- **Allow users to switch AI models** (e.g., **Gemini Flash** for speed vs. **Gemini Pro** for accuracy).  
- **Implement a backend with Node.js** to handle **CORS issues** and improve **data security**.  

---

## **Features**  

### **1. Smart Preference Setter (AI-powered input processing)**
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

## **Algorithm for Match Score Calculation**  

Each course receives a **match score (0-100%)**, calculated as follows:

### **1. Parameter Normalization**
Each numeric value is normalized between 0 and 1 using:
\[
\text{Normalized Value} = \frac{\text{Value} - \text{Min Value}}{\text{Max Value} - \text{Min Value}}
\]

### **2. Parameter Score Calculation**
Each parameter contributes to the total score. The formula for each parameter’s contribution:

\[
\text{Parameter Score} = \left( \frac{\text{Parameter Match Score} \times \text{Parameter Weight}}{\text{Total Weight}} \right) \times 100
\]

### **3. Topics of Interest Matching (Jaccard Similarity)**
For **Topics of Interest**, partial matching is computed using **word-based Jaccard similarity**:

\[
J(T_{\text{user}}, T_{\text{course}}) = \frac{|T_{\text{user}} \cap T_{\text{course}}|}{|T_{\text{user}} \cup T_{\text{course}}|}
\]

Where:  
- \( T_{\text{user}} \) = User-provided topic tags  
- \( T_{\text{course}} \) = Course topic tags  
- \( | \cdot | \) = Count of words  

Example:  
User input: **"Software Engineering"**  
Course tag: **"Software Security"**  
\[
J = \frac{1}{3} = 0.33
\]

If at least **one word matches**, the score is partially credited.

### **4. Final Match Score**
The final match score is calculated as the weighted sum of all parameter scores:

\[
\text{Final Score} = \sum_{i=1}^{n} (\text{Parameter Score}_i)
\]

---

## **Weaknesses & Limitations**
1. **Synthetic Dataset**  
   - The current dataset is **not real** and cannot be used by **University of Edinburgh (UoE) students**.
   - In a real scenario, data would need to come from **UoE’s official API**.

2. **AI Not Implemented in Decision-Making**  
   - The **matching algorithm is purely rule-based**.
   - AI **does not** influence the scoring process.
   - **Topics of Interest matching is non-AI-based**, meaning:
     - **"Software Engineering" ≠ "Web Development"**
     - Only **word overlap** is considered.

3. **Static CSV Database**  
   - Course data is **loaded from a static CSV file**.
   - In a real-world system, an **API should be used** to update courses **daily**.

4. **Gemini Flash Model Used (Low Latency, Lower Accuracy)**  
   - Uses **Google Gemini Flash** (faster, but may not be the best AI model).
   - Future versions could allow **switching models** for higher accuracy.
5. **CORS Violation in "Ask AI" Feature**  
   - The **"Ask AI"** feature fetches course details from the **DRPS website**, which is on a different domain.  
   - Browsers block these requests due to **CORS policies**, requiring users to install a **CORS extension** (e.g., **Allow CORS** for Chrome).  
   - In a **real-world scenario**, this could be resolved by using a **server-side proxy** (e.g., **Node.js with Express**) to handle requests securely.

---

## **Future Improvements**
- **Replace static CSV with an API for real-time course updates**.
- **Improve AI-based decision-making in match calculations**.
- **Enhance Topics of Interest matching with AI-based embeddings** (e.g., NLP similarity instead of simple Jaccard overlap).
- **Allow users to choose AI models for reasoning (Flash vs. Pro models).**

---

## **Installation Requirements**

To use the **"Ask"** feature, which fetches course details from the **DRPS website**, you need to bypass **CORS restrictions** since the DRPS page is on a different domain.  

### **Solution: Install a CORS Extension**  
1. **For Chrome:** Install [Allow CORS: Access-Control-Allow-Origin](https://chromewebstore.google.com/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf?hl=en)  
2. **For Firefox:** Install [CORS Everywhere](https://addons.mozilla.org/en-US/firefox/addon/cors-everywhere/)  

After installation, **enable the extension** before using the "Ask AI" feature.

---

## **Team Members:**
Shlok Gupta
Matvii Yatsenko
Yufeng Xia
Danylo Khrystenko
Daniel Hornung
---

## **References**
https://www.geeksforgeeks.org/
https://www.w3schools.com/
https://chatgpt.com/
https://ai.google.dev/
