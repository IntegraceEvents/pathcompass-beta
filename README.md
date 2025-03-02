---

# 📌 PATH Compass

## ⚡ TL;DR
**PATH Compass** is an AI-powered, interactive course recommendation system designed to help students effortlessly find ideal courses based on their preferences. Using natural language inputs, dynamic scoring, and explainable AI with Google Gemini, students get personalized course recommendations with clear justifications.

---

## 🎯 Why We Created PATH Compass
Choosing courses shouldn't feel like a guessing game. With thousands of options and limited guidance, students often struggle to pick the best courses for their goals.

### What makes PATH Compass special?
- 🧠 **AI-powered:** Converts natural language preferences into smart course recommendations.
- 🎛️ **Dynamic control:** Adjusts scoring factors in real time or lets AI handle it.
- 🔍 **Explainable:** Clearly shows why each course was recommended.
- ⚡ **Fast & lightweight:** Fully runs in-browser (currently using CSV datasets).
- 🚀 **Hackathon-ready:** Designed for rapid prototyping and real student impact.

---

## 🏗️ Features
| Feature                          | Status    |
|----------------------------------|-----------|
| ✅ Natural Language Input        | Working   |
| ✅ Course Scoring Algorithm      | Working   |
| ✅ AI-Powered Explanations       | Working   |
| ❌ Real Dataset Integration      | Planned   |
| ❌ API-Based Course Fetching     | Planned   |
| ❌ AI-Enhanced Match Scoring     | Planned   |

---

## 🧠 How It Works
1. **User Input**  
   Students describe their ideal courses in plain English. For example:
   > *“I prefer easy courses with high pass rates and fewer assessments.”*

2. **Preference Extraction**  
   Google Gemini Flash parses the description and assigns weighted importance to factors such as:
   - 📈 **Pass Rate**
   - 📚 **Coursework vs. Exam Ratio**
   - 🗓️ **Schedule Compatibility**
   - 👩‍🏫 **Instructor Rating**
   - 💬 **Topics of Interest**

3. **Scoring**  
   PATH Compass calculates a dynamic match score using these preferences. Users can further refine recommendations using intuitive sliders.

4. **Recommendation & Explanation**  
   Recommended courses are clearly ranked, with detailed AI-generated explanations (e.g., *“This course matches your desire for high coursework and low difficulty.”*)

---

## 💡 Why We Use Google Gemini Flash
- 🚀 **Speed:** Instant response for a seamless user experience.
- 🤖 **Contextual Understanding:** Accurately translates complex student preferences.
- 💰 **Cost-Effective:** Perfect for rapid prototyping and hackathon environments.

---

## 📊 Tech Stack
| Component      | Technology                  |
|----------------|-----------------------------|
| 🌐 Frontend    | HTML, CSS, JavaScript       |
| 📁 Data Storage| Static CSV (for prototype)  |
| 🧠 AI Engine   | Google Gemini Flash API     |
| ⚙️ Data Processing| PapaParse.js             |
| ☁️ Hosting     | GitHub Pages (Prototype)    |

---

## 📸 Screenshots
> _(Coming Soon)_
> **Example:**  
> ![Course Recommendation Example](https://your-screenshot-link.png)  
> ![AI Explanation Example](https://your-screenshot-link.png)

---

## 🔍 Algorithm Breakdown
- 📌 **Match Score Calculation** *(0-100%)*:
  - Parameters like **Pass Rate**, **Instructor Rating**, **Popularity**, and **Assessment Structure** are normalized and weighted.
  - **Topics of Interest** matched using **Jaccard Similarity** to accommodate partial matches.
  - Final score calculated as a weighted sum for clarity and accuracy.

---

## 🚀 Future Vision
- 🔄 **Live University API Integration:** Real-time course data updates.
- 🧠 **Full AI-Powered Scoring:** Transition to AI-driven recommendations beyond rule-based logic.
- 🌐 **Social Discovery:** Connect students for study groups based on matched courses.
- 🎓 **Graduation Path Optimization:** Suggest optimal course sequences for timely graduation or GPA maximization.
- 📈 **Demand Forecasting:** Predict course popularity and help students register strategically.

---

## 🛠️ Known Limitations
- ⚠️ **Synthetic Data:** Current dataset is placeholder; integration with official university data needed.
- ⚠️ **Static CSV:** Real-world implementation requires daily updates from APIs.
- ⚠️ **CORS Issues:** “Ask AI” feature currently needs a browser extension; future solution involves backend proxies.

---

## 🚧 Installation Requirements
To use the **"Ask AI"** feature (due to CORS restrictions):

- **Chrome:** [Allow CORS Extension](https://chromewebstore.google.com/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf?hl=en)
- **Firefox:** [CORS Everywhere](https://addons.mozilla.org/en-US/firefox/addon/cors-everywhere/)

Activate the extension before use.

---

## 🙌 Credits
### 🐘 **Edinburgh Elephants** (HackTheBurgh XI Team)
- **Shlok Gupta**
- **Matvii Yatsenko**
- **Yufeng Xia**
- **Danylo Khrystenko**
- **Daniel Hornung**

Powered by **Google Gemini AI**  
University of Edinburgh HackTheBurgh XI Challenge Project  
March 2025

---
