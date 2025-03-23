# 🧠 GynAI – AI Architecture Overview

## 🔹 1. Input Layer – Data Collection

### 👤 User Inputs:
- **Demographics:** age, sex assigned at birth, gender identity, menstrual cycle, weight, etc.
- **Symptoms:** chest pressure, fatigue, anxiety, dizziness, irregular periods, cold intolerance, etc.
- **Medical Records:** blood pressure, TSH, T3, T4, glucose, IgE, cholesterol, etc.

### 🔐 Security & Format:
- Inputs stored temporarily (if needed), with **encryption**
- Optional **on-device inference** depending on platform

---

## 🔹 2. Preprocessing Layer

### 🧪 Data Handling:
- **Normalization** of lab values into standardized units (SI, US)
- **Contextual Embedding** for symptoms using medical embeddings (e.g., BioBERT, ClinicalBERT)
- **Missing Data Imputation:** mean/mode fill-in or flagging if critical

---

## 🔹 3. Prediction Engine

### 🤖 A. Symptom-Based Models
- **Goal:** Estimate likelihood of conditions using symptoms + risk factors
- **Approach:** Logistic regression or shallow neural nets trained on synthetic EMR data (e.g., MIMIC-III, simulated Canadian datasets)

#### 🔍 Conditions Detected:
- **Heart Attack:** gender-specific symptom profiles
- **PCOS:** using Rotterdam criteria proxy
- **Thyroid Disorders:** based on symptoms + labs
- **Allergies:** symptom patterns + IgE markers

---

### 🧾 B. Lab-Based Threshold Models
Simple rule-based logic layered for validation:

| Condition         | Logic Example                                  |
|------------------|------------------------------------------------|
| Hypothyroidism    | TSH > X, T4 < Y                                |
| Hypertension      | BP > 140/90                                    |
| Diabetes          | Glucose > 126 (fasting)                        |
| Allergies         | IgE > 100                                      |

> 🔁 These rules **complement** the symptom-based predictions for **hybrid decision-making**.

---

## 🔹 4. Natural Language Layer (LLMs)

### 🧠 Models: Gemini / Cogere / GPT-type

**Input:** user responses, symptoms, lab data, prediction output

**Functions:**
- Translate raw predictions into **plain-language explanations**
- Auto-generate **doctor questions** (e.g., “Should I be tested for PCOS?”)
- Answer **health-related FAQs**

> 🧪 Example Prompt to LLM:  
> “Explain why this user might be at risk of hypothyroidism given their lab values (TSH: 6.1, T3: low, symptoms: cold intolerance, fatigue)”

---

## 🔹 5. Output Layer – UI Feedback

### 🧾 Risk Cards:
- **Red** = High Risk  
- **Yellow** = Mild Concern  
- **Green** = Normal

### 🗣️ User-Facing Output:
- Plain-language explanations of risks and conditions
- Recommended next steps
- “Ask your doctor” checklist auto-generated for user prep

---

## 🔹 6. Ethics & Bias Mitigation

### ⚖️ Built-In Protections:
- Reminder: **Predictions ≠ Diagnoses**
- Inclusive input: asks for **gender identity**, not just binary sex
- Monitors and adjusts for **demographic biases**
- Avoids **sexist assumptions** (e.g., “men feel pain, women feel anxiety”)

---

## 🛠️ Optional – Advanced Layer

### 📲 On-Device Inference:
- CoreML / TensorFlow Lite for privacy

### 🔁 Feedback Loop:
- User updates confirmed diagnosis
- Allows model **fine-tuning** (if user consent & privacy policy allows)

---

> 📌 *GynAI is designed for educational and assistive purposes only. No part of the system should be used as a substitute for professional medical advice.*
