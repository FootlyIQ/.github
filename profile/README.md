# ⚽ FootlyIQ

> Intelligent football analytics — redefined.

FootlyIQ is a full-stack web application built by our team as a part of our final project. It blends rich football data, intelligent visualizations, and advanced statistical insights into a responsive and user-friendly platform for fans, analysts, and fantasy managers.

### FootlyIQ Team Members
- [Gal Dvoršak](https://github.com/DvorsakGal)
- [Tanej Buhin](https://github.com/Tanejb)
- [Oliver Kunovski](https://github.com/cicooli)

🌍 **Live App**: [https://frontend-i3fb.onrender.com](https://frontend-i3fb.onrender.com)

---

## List of Contents
1. [Project Intro](#1-project-intro)
    - [Detailed Project Description](#detailed-project-description)
2. [Documentation](#2-documentation)
    - [Features](#features)
    - [Tech Stack](#tech-stack)
    - [Project Architecture](#project-architecture)
    - [Organization](#organization)
    - [Data Architecture](#data-architecture)
    - [Testing](#testing)
    - [GitHub Actions](#github-actions)
    - [Optimization](#optimization)
    - [Uporabniške zgodbe](#uporabniške-zgodbe)
3. [Navodila za namestitev lokalno](#3-navodila-za-namestitev-lokalno)
    - [Testno lokalno okolje](#testno-lokalno-okolje)
4. [User Walkthrough](#4-user-walkthrough)
    - [User Manual](#user-manual)
    - [Final Look](#final-look)
5. [Presentation](#5-presentation)

## 1. Project Intro
### Detailed Project Description
FootlyIQ is an intelligent football analytics web platform that combines live and historic match data, fantasy football, advanced visualizations, and machine learning insights. Users can explore detailed statistics like pass clustering, threat trends, and player performance directly from interactive dashboards. The app also includes a fantasy football section, where users can build and track teams based on real-world data. For informational purposes, FootlyIQ also provides betting insights with live odds. The platform is fully full-stack — with a React frontend, Flask backend, two Express.js microservices and a separate proxy.

## 2. Documentation
### Features
- 🟢 **Live Scores & Match Data**  
  Real-time match data, including lineups, substitutions, and in-play statistics (powered by external football APIs).
- 🧑‍🎓 **Extensive Team & Player Stats**  
  Team and player statistics for each match.
- 🎮 **Fantasy Football Section**  
  Pick your fantasy team and compete — driven by player performance and integrated with intelligent suggestions.
- 📈 **Interactive Visualizations**  
  Dynamic pitch-based visualizations built with custom SVG rendering and football data science conventions.
- 📊 **Event data insights using machine learning**  
  ML-powered features like pass clustering and xG.
- 💡 **Betting Insights** *(informational only)*  
  In betting section we show popular betting odds.

### Tech Stack
#### Backend
Application backend was made with Python, using the Flask framework, which helped us create REST API and communicate with our microservices, database and data lake. For a databse we went with Firebase (Firestore) which held user data, fantasy football data and match data. For data lake, the AWS S3 service was used. It served us as a storage of parquet files, which we used for displaying and visualizing our ML data. For retrieval and processing we used boto3, Duck DB and pandas For working with the database we used Firebase console. For testing of our APIs we mainly used Postman.

#### Frontend
- **React (JS) + Vite**
- **Tailwind CSS** for responsive UI
- **React Router** for SPA navigation

#### Matches and Bets microservices
- **Node.js with Express.js**

#### Deployment
For deployment we made a project on Render. This allowed us to deploy our project straight from the github repository.

### Project Architecture

### Organization
#### Communication
All communication within our team was conducted via a Discord server, except for the communication with the professor, which was conducted via MS Teams. We also conducted all group meetings and all remote work via the Discord server, where we helped each other with the screen sharing function.
#### Management and division of labor
For project managment we chose the SCRUM method, which is based on working in sprints. During the development we had 4 1-week long sprints. The project thus lasted from **07.05.2025 to 04.06.2025**. Before starting a new sprint we created new tasks, which we had to do in the next sprint.
For task assignment and keeping track we used Jira. We used a kanban board with backlog to keep track of our work.    

### Testing
We took care of testing by writing unit tests on the fly.

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


