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
    - [ML pipeline](#ml-pipeline)
    - [Code Review](#code-review)
    - [Use Case Diagram](#use-case-diagram)
    - [Activity Diagram for use of fantasy section](#activity-diagram-for-use-of-fantasy-section)
3. [User Walkthrough](#3-user-walkthrough)
    - [User Manual](#user-manual)
    - [Disclaimer](#disclaimer)
4. [Presentation](#4-presentation)

## 1. Project Intro
### Detailed Project Description
FootlyIQ is an intelligent football analytics web platform that combines live and historic match data, fantasy football, advanced visualizations, and machine learning insights. Users can explore detailed statistics like pass clustering, threat trends, and player performance directly from interactive dashboards. The app also includes a fantasy football section, where users can build and track teams based on real-world data. For informational purposes, FootlyIQ also provides betting insights with live odds. The platform is fully full-stack — with a React frontend, Flask backend, two Express.js microservices and a separate proxy.

---

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

<img src="https://github.com/user-attachments/assets/23b6d9c6-1a63-4a01-b142-a1e935389eee" alt="Render project" width="750"/>


### Project Architecture

The application follows a modular and scalable architecture with distinct separation of concerns across the frontend, backend, and external services:

- #### Frontend (Client Side)
  - Built using **React** to deliver a dynamic and responsive user experience.
  - Communicates with the backend via HTTP requests, primarily through RESTful APIs.

- #### Backend (Flask API)
  - Developed with **Flask (Python)**, acting as the central hub for handling frontend requests.
  - Manages data flow between the client, external services, and internal storage systems.

- #### Microservices (Node.js + Express)
  - Two microservices implemented in **Node.js** using **Express**:
    - **Matches Service**: Fetches real-time match data from the **football-data.org API**.
    - **Odds Service**: Retrieves betting odds from the **Odds API**.

- #### Home Server Proxy Service (Python)
  - A lightweight local proxy running 24/7 on a home server, written in **Python**.
  - Connects to the **Fantasy Premier League (FPL) API**, preprocesses or aggregates FPL data, and serves it to the Flask backend as needed.

<img src="https://github.com/user-attachments/assets/55752ad7-95ca-4b55-89d5-f1be49cb75c4" alt="Project architecture" width="750"/>

### Organization
#### Communication
All communication within our team was conducted via a Discord server, except for the communication with the professor, which was conducted via MS Teams. We also conducted all group meetings and all remote work via the Discord server, where we helped each other with the screen sharing function.
#### Management and division of labor
For project managment we chose the SCRUM method, which is based on working in sprints. During the development we had 4 1-week long sprints. The project thus lasted from **07.05.2025 to 04.06.2025**. Before starting a new sprint we created new tasks, which we had to do in the next sprint.
For task assignment and keeping track we used Jira. We used a kanban board with backlog to keep track of our work.  

<img src="https://github.com/user-attachments/assets/e64cbca9-df43-40e1-b4d1-e961f3b14128" alt="Sprint board" width="600"/>

### Data architecture
#### Firebase Firestore Database Structure
The application leverages **Google Firebase Firestore**, a scalable NoSQL database, for storing structured, real-time data.
  - #### Collections

    - ##### `match_vote_counts`
      - **Purpose**: Stores aggregated vote counts for matches.
      - **Fields**:
        - `away`: Number of votes for the away team (e.g., 1).
        - `draw`: Number of votes for a draw (e.g., 0).
        - `home`: Number of votes for the home team (e.g., 3).
      - **Example Document ID**: "524120".

    - ##### `match_votes`
      - **Purpose**: Stores individual votes for matches.
      - **Fields**:
        - `matchId`: String identifier for the match.
        - `timestamp`: Timestamp of the vote.
        - `user_id`: String identifier for the user.
        - `vote`: The vote value (e.g., "1").

    - ##### `user_favorites`
      - **Purpose**: Stores user-specific favorite data, such as favorite clubs and matches.
      - **Nested Structure**:
        - `clubs`:
          - `id`: Club identifier.
          - `crest`: URL to the club's crest image.
          - `name`: Club name.
          - `addedAt`: Timestamp of when the club was added.
        - `matches`:
          - `awayCrest`: URL to the away team's crest image.
          - `awayTeam`: Name of the away team.
          - `competition`: Competition name.
          - `addedAt`: Timestamp of when the match was added.

    - ##### `users`
      - **Purpose**: Stores user data.
      - **Fields**:
        - `createdAt`: Timestamp of user creation.
        - `email`: User's email address.
        - `name`: User's name.
        - `role`: User's role (e.g., "user").

    - ##### `votes`
      - **Purpose**: Stores users' voting data.
      - **Fields**:
        - `timestamp`: Timestamp of user's vote.
        - `user_id`: User's email address.
        - `vote`: User's vote (1, 2, or X).

#### S3 Data Lake
In the **Data Lake** files are organized by the medallion architecture principles. Therefore datasets used for machine learning **and** datasets containing data from ML used in the app are organized into 3 zones:
- **Bronze** containing raw datasets like stories.parquet
- **Silver** containing filtred/reduced datasets primarily used for machine learning purposes like passes_crosses.parquet
- **Gold** containing data ready for ad-hoc analyisi in Flask BE to be displayed to the user like xG_done_filtered.parquet

<img src="https://github.com/user-attachments/assets/776ade9f-7861-4fbb-aa09-c04ea14e2f88" alt="Data lake architecture" width="600"/>

### Testing
We took care of testing by writing unit tests on the fly. A workflow was also built, by using github actions, but we rather ran tests in the terminal of our project.    
We ensured proper testing by continuously writing unit tests throughout the development process. Tests were written for the following entities:    
- Matches
- Teams
- Players
- Match Stats

Unit tests were also written for all relevant utility functions and service integrations, including:
- API request handlers for matches, team squads, and statistics
- Firestore database interactions
- External service communication (e.g., FPL and microservices)

<img src="https://github.com/user-attachments/assets/f2addc47-9854-426f-98c4-e605971f6251" alt="Unit tests" width="600"/>


### ML pipeline
To offer users intelligent stats and visualizations we used pipeline with these steps:
- We gained our **datasets** in parquet or csv format
- For **machine learning** we used Jupyter Lab (locally) and Google Colab
- After successful machine learning we updated our datasets with columns derived from our **results gained**
- These final dataframes were then uploaded to our **S3 bucket** in parquet format
- For analysis and visualizations on client side these dataframes were fetched from the data lake via **boto3** library and processed with **pandas** library
- Given the type of data we chose this approach rather than deploying our ML models

<img src="https://github.com/user-attachments/assets/1569b735-f238-4f58-8d80-8609ee880c124" alt="ML pipeline" width="600"/>

### Code Review
For code optimization and code review we used SonarQube. This way we were able to review our code based on:    
- Maintainability
- Reliability
- Security

### Use Case Diagram

<img src="https://github.com/user-attachments/assets/89b8803c-d4a8-409d-92f2-218a75dc0776" alt="Activity diagram" width="600"/>

### Activity Diagram for use of fantasy section
<img src="https://github.com/user-attachments/assets/18205dad-1011-40d3-a309-330451e6d5e4" alt="Activity diagram" width="600"/>

---

## 3. User Walkthrough
### User Manual
For a complete tour of our app and tips on how to use it please refer to our User Manual accessible here:
https://github.com/FootlyIQ/.github/blob/main/UserManual_FootlyIQ.pdf

### Disclaimer❗
If you encounter problems when looking into clubs/players, especially in the Teams and Players section where search functionality is present. **DO NOT WORRY**. It's not an unexpected error. This is because our current plan with the api provider allows a certain number of calls per minute, and searching is pretty source intensive. Given that we spent over 60€ on the API alone, we didn't opt for further upgrades. So just wait a few moments and try again :) Sincerely, FootlyIQ team.    
Here is one example of such case:

<img src="https://github.com/user-attachments/assets/3184f9dd-3f0c-48df-a5e7-0bacc142b529" alt="Activity diagram" width="600"/>

---

## 4. Presentation
To look at the powerpoint presentation please follow this link:

https://univerzamb-my.sharepoint.com/:p:/g/personal/oliver_kunovski_student_um_si/EYP928-E0oZOm-EUh7Wj5-gBWz6GnkAZxhGxOlKYtpkJ2Q?e=GhbDbD


