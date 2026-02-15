# 🛡️ Abhaya | Safe Route AI (Bhubaneswar Edition)

A comprehensive, production-ready routing system designed for **safety-aware navigation**. While standard GPS apps optimize only for the shortest travel time, Abhaya introduces a context-aware AI routing engine that calculates the **safest possible path** by evaluating historical risk data, time of day, and environmental conditions.

Built specifically for urban environments (currently mapped to Bhubaneswar, Odisha), this tool empowers users—especially women navigating at night—to make informed, secure travel decisions.

---

## ✨ Key Features

* **⚡ Fastest vs. 🛡️ Safest Routing Engine:** * *Fastest:* Standard shortest-path routing based on physical distance.
    * *Safest:* Uses a custom-weighted **Dijkstra's Algorithm** to route users around high-risk zones, preferring well-lit, highly populated, or historically safer streets.
* **🌙 Context-Aware Safety Multipliers:** The backend dynamically scales road danger levels based on the user's current context. Nighttime increases base risk by 1.6x, and adverse weather (like fog) multiplies risk by up to 2.0x.
* **🚨 Live GPS SOS Dispatch:** A pulsing emergency button that utilizes the HTML5 Geolocation API to instantly pull the user's exact real-world coordinates and package them into a JSON payload for emergency contacts and authorities.
* **💎 Dynamic Glassmorphism UI:** A premium, frosted-glass interface that automatically switches between a bright "Positron" Light Theme and a high-contrast "Dark Matter" Night Theme based on the user's selected time context.

---

## 🧠 System Architecture & Algorithm

Unlike basic API-wrapper apps, Abhaya computes its safe routes **locally via graph theory**.

1.  **Graph Generation (`OSMnx` & `NetworkX`):** The backend downloads the entire OpenStreetMap road network for the city and constructs a mathematical graph where every road intersection is a node, and every street is an edge.
2.  **Risk Assignment:** Base risk scores are assigned to every street segment. 
3.  **Dynamic Pathfinding:** When a user requests the "Safest" route, the backend applies a custom weight function:
    `Safe Weight = Length * (1.0 + (Base_Risk * Time_Multiplier * Weather_Multiplier))`
4.  The system runs **Dijkstra's Algorithm** against these dynamic weights to mathematically guarantee the safest physical path to the destination.

---

## 🛠️ Technology Stack

**Frontend:**
* HTML5 / CSS3 / Vanilla JavaScript
* **Leaflet.js** (Interactive mapping & GeoJSON rendering)
* **CartoDB** (Dynamic Positron & Dark Matter map tiles)
* **Bootstrap 5** (Responsive layout)

**Backend:**
* **FastAPI** (High-performance Python web framework)
* **OSMnx** (Spatial data extraction and graph generation)
* **NetworkX** (Complex network analysis and routing algorithms)
* **Scikit-learn** (Spatial k-d tree nearest-node calculations)
* **Uvicorn** (ASGI server)

---

## 🚀 How to Run Locally

### Prerequisites
* Python 3.10+
* Internet connection (to fetch map tiles and geocoding)

### 1. Backend Setup
Clone the repository and navigate to the backend directory:
```bash
git clone [https://github.com/Maahivarma/abhaya-safe-route-ai.git](https://github.com/Maahivarma/abhaya-safe-route-ai.git)
cd abhaya-safe-route-ai