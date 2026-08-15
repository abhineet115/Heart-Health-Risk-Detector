# ❤️ Heart Health Risk Detector

[![GitHub Pages](https://img.shields.io/badge/Live_Demo-GitHub_Pages-brightgreen?style=for-the-badge&logo=github)](https://abhineet115.github.io/Heart-Health-Risk-Detector/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_&_Firestore-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Chart.js](https://img.shields.io/badge/Chart.js-Data_Visualization-FF6384?style=for-the-badge&logo=chart.js&logoColor=white)](https://www.chartjs.org/)

An interactive, responsive web application designed to help individuals evaluate their cardiovascular health risk based on personal vitals, lifestyle habits, medical history, and optional lab biomarkers.

🔗 **Live Demo:** [https://abhineet115.github.io/Heart-Health-Risk-Detector/](https://abhineet115.github.io/Heart-Health-Risk-Detector/)

---

## 📋 Table of Contents

- [🌟 Features](#-features)
- [🧮 How It Works & Risk Factors](#-how-it-works--risk-factors)
- [🛠️ Tech Stack](#️-tech-stack)
- [🚀 Quick Start (Local Setup)](#-quick-start-local-setup)
- [🌐 Hosting on GitHub Pages](#-hosting-on-github-pages)
- [🔥 Firebase Setup & Configuration](#-firebase-setup--configuration)
- [📁 Project Structure](#-project-structure)
- [⚠️ Medical Disclaimer](#️-medical-disclaimer)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🌟 Features

### 🫀 Comprehensive Risk Assessment
- Multi-factorial assessment evaluating personal physical metrics, habits, and clinical indicators.
- Instant score computation on a calibrated scale (0–60) with clear Low, Moderate, and High risk classifications.
- Dynamic animated visual risk meter.

### 🤖 AI 10-Year Risk Simulation & Precautions
- Simulated predictive 10-year cardiovascular risk projection.
- Dynamic, personalized actionable recommendations and lifestyle precaution steps based on specific risk drivers.
- Direct **Consult a Doctor** inquiry flow.

### 👤 User Authentication & Account Management
- Seamless Firebase Authentication (Email/Password registration & login, Google Sign-In, and password recovery).
- User profile tracking and secure session state.

### 📊 Health Trends Dashboard & Charting
- Visual historical tracking powered by **Chart.js** with interactive health progress trendlines.
- Automated summary insights highlighting improvements or areas of concern.
- Pagination for viewing historical assessments.

### 💾 Auto-Save & Draft Recovery
- Real-time form progress tracking with draft caching in `localStorage`.
- Automatic prompt to restore unsubmitted drafts.

### 🔒 Privacy & Data Portability
- Secure cloud storage using **Firebase Firestore** with user-level isolation.
- Complete data export functionality (JSON format).
- Complete data privacy options: single record deletion, bulk record purging, and account deletion.

---

## 🧮 How It Works & Risk Factors

The calculator aggregates risk points across four primary domains:

| Category | Evaluated Parameters |
| :--- | :--- |
| **Personal Vitals** | Age, Gender, Weight, Height (Calculated BMI), Waist Circumference, Socio-economic status |
| **Lifestyle Habits** | Daily step count, Weekly fast-food consumption, Exercise hours, Alcohol intake, Smoking status, Average sleep duration, Stress levels |
| **Medical History** | Family history of cardiovascular disease, Systolic & Diastolic Blood Pressure, Resting Heart Rate, Known Hypertension, Diabetes, Existing conditions |
| **Optional Blood Panel** | Total Cholesterol (mg/dL), Red Blood Cell count (RBC), White Blood Cell count (WBC) |

### Risk Classification:
- 🟢 **Low Risk (0–19 points):** Optimal lifestyle and vitals; keep up healthy habits.
- 🟡 **Moderate Risk (20–39 points):** Manageable risk factors identified; lifestyle adjustments recommended.
- 🔴 **High Risk (40–60 points):** Significant cardiovascular risk markers; prompt medical consultation advised.

---

## 🛠️ Tech Stack

- **Frontend:** HTML5, Modern Vanilla JavaScript (ES6 Modules)
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) (CDN) + Custom CSS transitions & glassmorphism
- **Data Visualization:** [Chart.js](https://www.chartjs.org/)
- **Backend & Cloud Services:** [Firebase](https://firebase.google.com/)
  - **Firebase Authentication:** User management (Google OAuth & Email/Password)
  - **Cloud Firestore:** Real-time NoSQL database for assessment history

---

## 🚀 Quick Start (Local Setup)

To run this application locally without any complicated build steps:

### 1. Clone the repository
```bash
git clone https://github.com/abhineet115/Heart-Health-Risk-Detector.git
cd Heart-Health-Risk-Detector
```

### 2. Start a local HTTP server
Because the project uses ES6 JavaScript modules (`type="module"`), it should be served via a local web server rather than opened directly as a file.

**Using Python:**
```bash
# Python 3
python -m http.server 8080
```

**Using Node.js (`npx`):**
```bash
npx serve -l 8080 .
```

**Using VS Code:**
- Install the **Live Server** extension.
- Right-click `index.html` and select **"Open with Live Server"**.

### 3. Open in Browser
Navigate to `http://localhost:8080/index.html` in your web browser.

---

## 🌐 Hosting on GitHub Pages

This repository is ready to be hosted on **GitHub Pages** with zero build configuration:

1. Push your repository to GitHub:
   ```bash
   git add .
   git commit -m "Update application and documentation"
   git push origin main
   ```
2. Go to your repository on GitHub:
   - Click on **Settings** (top tabs).
   - In the left sidebar, click on **Pages** (under *Code and automation*).
3. Under **Build and deployment**:
   - **Source:** Select `Deploy from a branch`.
   - **Branch:** Select `main` and folder `/ (root)`.
   - Click **Save**.
4. After 1–2 minutes, your live site will be accessible at:
   ```
   https://<your-username>.github.io/Heart-Health-Risk-Detector/
   ```

---

## 🔥 Firebase Setup & Configuration

To connect the application to your own Firebase backend:

1. Create a project in the [Firebase Console](https://console.firebase.google.com/).
2. Enable **Authentication**:
   - Enable **Email/Password** provider.
   - Enable **Google** sign-in provider.
   - In **Authorized Domains**, add `localhost`, `127.0.0.1`, and your GitHub Pages domain (`<username>.github.io`).
3. Create a **Cloud Firestore Database**:
   - Apply the security rules from [`firestore.rules`](firestore.rules).
4. Copy the template configuration file:
   ```bash
   cp firebase-config.example.js firebase-config.js
   ```
5. Fill in your project keys in `firebase-config.js`. (Note: `firebase-config.js` is included in `.gitignore` so your personal keys are never committed to public repositories).
6. Read [`SECURITY.md`](SECURITY.md) for full instructions on setting API key HTTP referrer restrictions in Google Cloud Console.

---

## 📁 Project Structure

```text
Heart-Health-Risk-Detector/
├── index.html                  # Main HTML layout, navigation, forms, modals & templates
├── script.js                   # Core application logic, risk scoring algorithms & Firebase integration
├── style.css                   # Custom animations, meter UI styling, responsive overrides
├── firebase-config.example.js  # Public template for Firebase credentials
├── firestore.rules             # Production database access rules
├── SECURITY.md                 # Security hardening & API key restriction guide
└── README.md                   # Project documentation and setup guide
```

---

## ⚠️ Medical Disclaimer

> **IMPORTANT:** This application is created for educational and informational purposes only. It is **NOT** a medical diagnostic tool and should **NEVER** replace professional medical advice, clinical diagnosis, or treatment. 
> 
> Always seek the advice of your physician or other qualified health provider with any questions you may have regarding a medical condition or symptoms such as chest pain, shortness of breath, or palpitations.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
