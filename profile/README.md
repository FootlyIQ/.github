# ⚽ FootlyIQ

> Intelligent football analytics — redefined.

FootlyIQ is a full-stack web application built by a team of undergraduate Computer Science students as part of their final project. It blends rich football data, intelligent visualizations, and advanced statistical insights into a responsive and user-friendly platform for fans, analysts, and fantasy managers.

🌍 **Live App**: [https://frontend-i3fb.onrender.com](https://frontend-i3fb.onrender.com)

---

## 🚀 Features

- 📊 **Advanced Pass Clustering**  
  ML-powered clustering of passes across top football teams using precomputed KMeans models on event-level datasets.

- 🟢 **Live Scores & Match Data**  
  Real-time match data, including lineups, substitutions, and in-play statistics (powered by external football APIs).

- 🎮 **Fantasy Football Section**  
  Pick your fantasy team and compete — driven by player performance and integrated with intelligent suggestions.

- 💡 **Betting Insights** *(informational only)*  
  Based on model outputs, we show how our predictions compare to popular betting odds (for educational use).

- 📈 **Interactive Visualizations**  
  Dynamic pitch-based visualizations built with custom SVG rendering and football data science conventions.

---

## 🧠 Tech Stack

### Frontend
- **React + Vite**
- **Tailwind CSS** for responsive UI
- **React Router** for SPA navigation
- **Dark/light mode** toggle
- Hosted on **Render**

### Backend
- **Flask** REST API
- **DuckDB** for in-place SQL over S3-hosted Parquet files
- **Pandas** for ad-hoc ML analytics
- **boto3** to fetch data from **AWS S3**
- **Deployed on Render backend service**

### Storage & Data
- **AWS S3**: all analytics and raw data stored as `.parquet`
- **MongoDB**: semi-structured football data (teams, players, predictions, fantasy teams)
- **Firebase**: authentication and secure user data handling

---

## 📂 Project Structure (Backend)


