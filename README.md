# Kakuma Health Tracker

Kakuma Health Tracker is a web-based health data visualization tool designed to monitor malaria and water-borne disease cases across different zones within Kakuma Refugee Camp.
It leverages Firebase Firestore as an external API to fetch real-time health statistics and provides users with interactive tools for searching, sorting, filtering, and visualizing data.

This project was built as part of an academic assignment focused on API usage, meaningful application design, and real-world deployment using load-balanced web servers.

---

## 📌 Table of Contents

* [Project Overview](#project-overview)
* [Features](#features)
* [Technology Stack](#technology-stack)
* [External API Used](#external-api-used)
* [Screenshots](#screenshots)
* [How to Run Locally](#how-to-run-locally)
* [Deployment Guide](#deployment-guide)

  * [1. Prepare Your Web Servers](#1-prepare-your-web-servers)
  * [2. Deploy to Web01 and Web02](#2-deploy-to-web01-and-web02)
  * [3. Configure Load Balancer](#3-configure-load-balancer)
  * [4. Verify Load Balancing](#4-verify-load-balancing)
* [Error Handling](#error-handling)
* [Folder Structure](#folder-structure)
* [API Attribution](#api-attribution)
* [Challenges and Solutions](#challenges-and-solutions)
* [Demo Video](#demo-video)
* [Author](#author)

---

##  Project Overview

Kakuma Health Tracker aims to provide practical value by helping health workers and decision-makers visualize disease trends in Kakuma Refugee Camp.

The application retrieves zone-level disease statistics from Firebase Firestore, displays totals, and renders interactive bar charts using Chart.js. It also allows:

- Searching health zones
- Sorting in ascending/descending order
-Filtering by malaria or water-borne cases
-Viewing aggregated statistics

---

 Features

1. Real-time data from Firebase (external API)

Data is fetched directly from Firestore’s `"health_zones"` collection.

2. Interactive data tools

- Search Zones
- Sort by malaria / water-borne cases
-Toggle ascending/descending order

3. Data visualization

- Dynamic chart generated via **Chart.js**
- Auto-updates when user filters or sorts data

4. Responsive UI

Clean and intuitive interface using vanilla HTML, CSS, and JS.

5. Fully deployed on two webservers with a load balancer

Traffic is distributed by LB01 → Web01/Web02.

---

## 🛠 Technology Stack

| Component     | Technology                  |
| ------------- | --------------------------- |
| Frontend      | HTML, CSS, JavaScript       |
| API           | Firebase Firestore          |
| Charts        | Chart.js                    |
| Servers       | Ubuntu 20.04 Web Servers    |
| Load Balancer | HAProxy / Nginx             |
| Hosting       | Provided ALX/School Servers |

---

## 🌐 External API Used

Firebase Firestore (Database API)

Firestore is used as the external API to fetch structured health zone data:

* `malaria_count`
* `waterborne_count`
* `zone`

API documentation:
[https://firebase.google.com/docs/firestore](https://firebase.google.com/docs/firestore)

#### 🔒 API Key Safety

Although the Firebase API key is safe for frontend usage, best practices were applied:

* No private server keys exposed
* Project rules configured in Firebase Console
* `.gitignore` prevents sensitive files from being committed

---

## 🖼 Screenshots

*(Add screenshots after deployment — recommended sections included.)*

---

## 🖥 How to Run Locally

### 1. Clone the repository

```
git clone git@github.com:jamesdeng462/health-tracker.git
```

### 2. Navigate into the project

```
cd health-tracker
```

### 3. Open the application

You can open it directly in a browser:

```
open index.html
```

or
Double-click `index.html`.

### 4. Ensure Firebase Access

No additional setup is needed — Firestore rules allow safe read access.

---

## 🚀 Deployment Guide

Below is the full deployment procedure used for Web01, Web02, and LB01.

---

## 1️⃣ Prepare Your Web Servers

Servers provided:

| Server        | IP                 | Status  |
| ------------- | ------------------ | ------- |
| Web01         | **44.204.8.150**   | running |
| Web02         | **44.201.188.183** | running |
| Load Balancer | **44.206.250.200** | running |

### Update & install web server:

```
sudo apt update
sudo apt install nginx -y
```

---

## 2️⃣ Deploy to Web01 and Web02

### Upload project files:

```
scp -r * ubuntu@44.204.8.150:/var/www/html/
scp -r * ubuntu@44.201.188.183:/var/www/html/
```

### Set permissions:

```
sudo chown -R www-data:www-data /var/www/html/
sudo systemctl restart nginx
```

Your application now runs at:

* [http://44.204.8.150](http://44.204.8.150)
* [http://44.201.188.183](http://44.201.188.183)

---

## 3️⃣ Configure Load Balancer (LB01)

### Install HAProxy:

```
sudo apt update
sudo apt install haproxy -y
```

### Edit configuration:

```
sudo nano /etc/haproxy/haproxy.cfg
```

### Add this block:

```
frontend http_front
    bind *:80
    default_backend web_servers

backend web_servers
    balance roundrobin
    server web01 44.204.8.150:80 check
    server web02 44.201.188.183:80 check
```

### Restart HAProxy:

```
sudo systemctl restart haproxy
```

Your app is now load-balanced at:

👉 **[http://44.206.250.200](http://44.206.250.200)**

---

## 4️⃣ Verify Load Balancing

Reload the LB URL several times:

```
http://44.206.250.200
```

Check:

* Both servers respond
* No errors
* Chart loads
* Firebase data displays

---

## ⚠ Error Handling

The application includes:

* Try/catch wrappers around Firestore data fetching
* Clear user feedback if data fails to load
* Graceful fallback when search returns zero results
* Chart auto-destroys before re-rendering (avoids memory leaks)

---

## 📂 Folder Structure

```
health-tracker/
│
├── index.html
├── README.md
└── assets/ (optional future use)
```

---

## 🙏 API Attribution

This project uses the following external API:

Google Firebase Firestore

* [https://firebase.google.com/docs/firestore](https://firebase.google.com/docs/firestore)
* Used for real-time data fetching
* All rights belong to Google LLC

Chart.js

* [https://www.chartjs.org/](https://www.chartjs.org/)
* Used for graph visualization

Both are credited as required by the assignment rubric.

---

 🧠 Challenges and Solutions

 1. **Ensuring Firebase works on remote Nginx servers**

* Solved by allowing HTTPS calls and enabling CORS on Firestore.

2. Load balancer not forwarding traffic**

* Fixed by adding proper health checks in HAProxy.

3. Chart.js re-render bug

* Destroyed chart before re-creating to prevent overlay duplication.

 4. Preventing empty search results from breaking chart

* Added fallback messaging + conditional chart updates.

---

## 🎬 Demo Video

A short demo video (≤2 minutes) will showcase:

* Application running locally
* Deployment on Web01 & Web02
* Load balancer access via `44.206.250.200`
* Sorting, searching, and chart rendering

🎥 [Demo Link  https://youtu.be/yntoecshQ3A

---

## 👤 Author

James Deng
GitHub: [https://github.com/jamesdeng462](https://github.com/jamesdeng462)
Project Repo: [https://github.com/jamesdeng462/health-tracker](https://github.com/jamesdeng462/health-tracker)

---


