# 🏭 AI Enterprise Digital Twin Decision Agent

> **Simulate → Optimize → Decide — before it costs you real money.**

An intelligent **Enterprise Digital Twin** platform that creates a virtual replica of a business (factory / warehouse / retail), runs **time-based simulations**, uses a **Reinforcement Learning agent (PPO)** to recommend optimal business decisions, streams **IoT sensor data**, and leverages **Google Gemini LLM** to explain results in plain human language.

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)
![React](https://img.shields.io/badge/React-18-61DAFB.svg)
![MySQL](https://img.shields.io/badge/MySQL-8.0-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-In%20Development-orange.svg)

---

## 📸 Screenshots

> _Screenshots will be added soon — dashboard, simulation runner, AI agent view, and Gemini insights._

<!-- 
![Dashboard](docs/screenshots/dashboard.png)
![Simulation](docs/screenshots/simulation.png)
![Agent](docs/screenshots/agent.png)
![Insights](docs/screenshots/insights.png)
-->

---

## 🎯 Problem Statement

Modern enterprises (factories, warehouses, retail chains) make critical decisions daily — hiring workers, buying machines, restocking inventory, adjusting production. A wrong decision can cost **lakhs of rupees** and weeks of recovery.

Traditional ERPs tell you **what happened**. They don't tell you **what could happen**.

This project solves that by building a **safe digital environment** where business decisions can be tested, simulated, and optimized **before** implementation.

---

## 💡 Solution Overview

The system creates a **Digital Twin** of an enterprise with entities like:

- 🏭 **Machines** — capacity, health, breakdowns
- 👷 **Workers** — productivity, shifts, cost
- 📦 **Inventory** — stock levels, reorder points
- 🛒 **Orders** — demand, priority, deadlines
- 💰 **Finance** — revenue, cost, profit

Over this twin, an **RL agent (PPO)** learns to make optimal decisions. **IoT sensors** feed live data. **Gemini LLM** converts complex outputs into human-readable insights.

---

## ✨ Key Features

### 🏭 Digital Twin Engine
- Virtual replica of an enterprise with realistic entity behavior
- Time-step simulation (hourly / daily)
- Random real-world events: machine breakdowns, demand spikes, supplier delays
- KPI tracking: profit, throughput, utilization, cost, downtime

### 🤖 Reinforcement Learning Agent
- Custom **Gymnasium** environment wrapping the digital twin
- **PPO (Proximal Policy Optimization)** via Stable-Baselines3
- Trained on **CPU** (lightweight, no GPU required)
- Learns optimal policies: *when to hire, restock, buy machines, shutdown*
- Continuously improves with more episodes

### 📡 IoT Sensor Layer (Simulated)
- Mock sensor stream: temperature, vibration, output rate, power usage
- Real-time data feed via REST + WebSocket
- Device registry with health status
- Feeds live data into the digital twin

### ✨ Gemini LLM Integration
- Converts raw simulation numbers → natural language insights
- Answers "what-if" questions in chat format
- Generates executive summaries for decision reports

**Example output:**
> *"Adding 2 machines increases profit by 18% but raises maintenance cost by 12%. Net gain: +6%. Recommended action: proceed."*

### 🎨 Modern React Dashboard
- Beautiful dark-mode UI with glassmorphism
- Live KPI tiles with animations
- Interactive charts (line, bar, radar, heatmap)
- Simulation runner with parameter sliders
- AI decision feed with confidence scores
- Gemini insight chat interface
- Historical decisions timeline

### 🗄️ SQL Database
- Stores enterprises, sensors, simulations, decisions, agent runs, insights
- Full history & audit trail
- Fast aggregated queries for dashboard

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Python 3.10+, FastAPI, SQLAlchemy, Alembic, Pydantic |
| **RL / AI** | Stable-Baselines3 (PPO), Gymnasium, NumPy, Pandas |
| **LLM** | Google Gemini API (`google-generativeai`) |
| **Frontend** | React 18, Vite, TailwindCSS, Recharts, Framer Motion, Axios |
| **Database** | MySQL 8.0 |
| **IoT** | Python async mock simulator (REST + WebSocket) |
| **DevOps** | Docker, Uvicorn, Git |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    REACT UI (Frontend)                   │
│   Dashboard │ Simulation │ Agent │ Sensors │ Insights    │
└───────────────────────┬─────────────────────────────────┘
                        │ REST + WebSocket
┌───────────────────────▼─────────────────────────────────┐
│                  FASTAPI BACKEND                         │
│  Routers → Services → Models → SQLAlchemy → MySQL        │
├─────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │
│  │ DIGITAL TWIN │←→│  RL AGENT    │←→│ GEMINI LLM   │   │
│  │   ENGINE     │  │  (PPO)       │  │ EXPLAINER    │   │
│  └──────┬───────┘  └──────────────┘  └──────────────┘   │
│         │                                                │
│  ┌──────▼───────┐                                        │
│  │  IoT MOCK    │  ← Simulated sensor stream             │
│  │  SENSORS     │                                        │
│  └──────────────┘                                        │
└─────────────────────────────────────────────────────────┘
```

---

## 🔄 How It Works

1. **User** opens the React dashboard
2. **Selects a scenario** (factory_default, warehouse_stress, etc.)
3. **Clicks "Run Simulation"** → request goes to FastAPI
4. **Digital Twin Engine** runs the simulation for N time steps
5. **IoT mock layer** injects sensor data (temperature, output, etc.)
6. **RL Agent** observes state → recommends best action
7. **Simulation results** stored in **MySQL**
8. **Gemini API** generates natural language explanation
9. **Frontend** displays charts, KPIs, decisions, and insights
10. **User** compares scenarios, takes informed decision ✅

---

## 📁 Project Structure

```
ai-enterprise-digital-twin/
│
├── README.md
├── .gitignore
├── .env.example
├── docker-compose.yml
│
├── docs/
│   ├── architecture.md
│   ├── api-reference.md
│   ├── simulation-model.md
│   ├── rl-agent-design.md
│   └── screenshots/
│
├── backend/
│   ├── requirements.txt
│   ├── .env
│   ├── main.py
│   ├── config.py
│   ├── database.py
│   │
│   ├── app/
│   │   ├── models/            # SQLAlchemy models
│   │   ├── schemas/           # Pydantic schemas
│   │   ├── routers/           # API routes
│   │   ├── services/          # Business logic
│   │   ├── digital_twin/      # Simulation engine
│   │   ├── rl_agent/          # RL agent (PPO)
│   │   ├── llm/               # Gemini integration
│   │   ├── iot/               # IoT mock layer
│   │   ├── utils/             # Helpers
│   │   └── core/              # Core config
│   │
│   ├── alembic/               # DB migrations
│   ├── scripts/               # Utility scripts
│   ├── tests/                 # Unit tests
│   └── data/                  # Scenarios & samples
│
├── frontend/
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── index.html
│   │
│   └── src/
│       ├── api/               # API client
│       ├── components/        # Reusable components
│       ├── pages/             # Route pages
│       ├── layouts/           # Layouts
│       ├── routes/            # Routing
│       ├── hooks/             # Custom hooks
│       ├── context/           # Global state
│       ├── store/             # Zustand/Redux
│       ├── utils/             # Helpers
│       └── styles/            # CSS
│
└── database/
    ├── schema.sql
    ├── seed.sql
    ├── migrations/
    ├── erd/
    └── backups/
```

---

## ⚙️ Installation & Setup

### Prerequisites

- **Python** 3.10+
- **Node.js** 18+
- **MySQL** 8.0+
- **Git**
- **Gemini API Key** — get it free from [Google AI Studio](https://aistudio.google.com/app/apikey)

### 1. Clone the Repository

```bash
git clone https://github.com/vishakha2121/AI-Enterprise-Digital-Twin-Decision-Agent.git
cd AI-Enterprise-Digital-Twin-Decision-Agent
```

### 2. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Setup environment variables
cp .env.example .env
# Edit .env and add your GEMINI_API_KEY and DATABASE_URL
```

### 3. Database Setup

```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE digital_twin_db;

# Import schema
mysql -u root -p digital_twin_db < database/schema.sql
```

### 4. Run Backend

```bash
uvicorn main:app --reload --port 8000
```

Backend running at → `http://localhost:8000`
API docs at → `http://localhost:8000/docs`

### 5. Frontend Setup

```bash
cd frontend
npm install
cp .env.example .env
npm run dev
```

Frontend running at → `http://localhost:5173`

---

## 🔌 API Endpoints (Sample)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/enterprises` | List all enterprises |
| POST | `/api/enterprises` | Create new enterprise |
| GET | `/api/sensors/live` | Live IoT sensor data |
| POST | `/api/simulations/run` | Run a simulation |
| GET | `/api/simulations/{id}` | Get simulation results |
| POST | `/api/agent/recommend` | Get RL agent recommendation |
| POST | `/api/insights/explain` | Generate Gemini explanation |
| GET | `/api/dashboard/summary` | Dashboard KPIs |

Full API reference → [docs/api-reference.md](docs/api-reference.md)

---

## 🧪 Example Use Case

> **Scenario:** A factory has 10 machines and 50 workers. Demand is rising. Should the manager buy 2 more machines?

**Without this project:** Manager guesses → buys → loss/profit after months

**With this project:**
1. Manager runs simulation with "add 2 machines"
2. Digital twin simulates 30 days → profit +18%, maintenance +12%, net +6%
3. RL agent confirms it's the optimal action
4. Gemini explains: *"Recommended. Net gain +6% over 30 days. Break-even in 14 days."*
5. Manager decides **confidently** — decision made in 2 minutes, not 2 months ✅

---

## 🎯 Project Scope

### ✅ In Scope (Practice / Learning Project)
- Single-enterprise digital twin
- Simulated IoT sensors (no real hardware)
- PPO agent on CPU (lightweight)
- Gemini for insights & explanations
- Local MySQL database
- Modern React dashboard
- REST + WebSocket APIs

### ❌ Out of Scope (Production would need these)
- Multi-tenant SaaS architecture
- Real IoT hardware integration
- Distributed training / GPU clusters
- Advanced authentication & RBAC
- Cloud deployment (AWS/GCP)
- Enterprise security & compliance

> **Note:** This is a **learning / portfolio project**, not a production system. Focus is on clean architecture, working AI pipeline, and great UI.

---

## 🧠 Learning Outcomes

By building this project, one learns:

- ✅ How to design a **digital twin** architecture
- ✅ How to build a **custom Gym environment** for RL
- ✅ How to train **PPO on CPU** efficiently
- ✅ How to integrate **LLMs (Gemini)** for explainability
- ✅ How to build **real-time IoT simulation**
- ✅ How to design **scalable FastAPI backends**
- ✅ How to build **modern, animated React dashboards**
- ✅ How to structure a **full-stack AI project**

---

## 🚀 Future Enhancements

- 🔐 Add authentication (JWT)
- ☁️ Deploy on cloud (Render + Vercel)
- 🧠 Add multi-agent RL (cooperative decisions)
- 📊 Add forecasting models (time-series)
- 🎙️ Add voice-based query (Gemini + TTS)
- 🔗 Integrate real IoT devices (MQTT)
- 📱 Build mobile app (React Native)
- 🏢 Multi-enterprise support

---

## 🤝 Contributing

This is a personal learning project. Suggestions and feedback are welcome!

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👩‍💻 Author

**Vishakha**

- GitHub: [@vishakha2121](https://github.com/vishakha2121)
- Project Link: [AI-Enterprise-Digital-Twin-Decision-Agent](https://github.com/vishakha2121/AI-Enterprise-Digital-Twin-Decision-Agent)

---

## 🙏 Acknowledgements

- [FastAPI](https://fastapi.tiangolo.com/)
- [Stable-Baselines3](https://stable-baselines3.readthedocs.io/)
- [Google Gemini API](https://ai.google.dev/)
- [React](https://react.dev/)
- [TailwindCSS](https://tailwindcss.com/)
- [Recharts](https://recharts.org/)

---

⭐ **If you found this project interesting, please give it a star!** ⭐