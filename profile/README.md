<div align="center">

<img src="assets/wasla_logo.png" alt="WASLA Logo" width="320"/>

# WASLA | وصلة

**AI-Powered Blood Donation & Blood Supply Management Ecosystem**

وصلة منظومة ذكية متكاملة لإدارة التبرع بالدم وسلاسل إمداد الدم بالذكاء الاصطناعي

![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/Frontend-React-61DAFB?logo=react&logoColor=black)
![SQLAlchemy](https://img.shields.io/badge/ORM-SQLAlchemy-D71F00)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB?logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Development-orange)

</div>

---

## 📌 About

WASLA is not just a donor-finder app. It is an **AI-powered ecosystem** that connects **donors, patients, hospitals, doctors, laboratories, and blood banks** in a single closed loop.

The core idea is to shift blood donation from a **reactive** process (searching only after an emergency) to a **proactive** one that predicts demand, prioritizes urgent cases, and ranks the most suitable donors, while keeping **doctors, not AI, as the final authority** on medical decisions.

> 🇪🇬 **بالعربي:** وصلة مش مجرد تطبيق للتبرع بالدم، دي منظومة ذكية بتربط المتبرعين والمرضى والمستشفيات والدكاترة والمعامل وبنوك الدم في دورة واحدة. الذكاء الاصطناعي بيساعد في الترتيب والتوقع والتنبيه، لكن القرار الطبي النهائي دايمًا للدكتور.

## ✨ Key Features

| Feature | Description |
|---|---|
| 🎯 **AI Donor Matching & Ranking** | Ranks compatible donors by medical compatibility, distance, availability, and response history |
| 🚨 **Urgency Scoring** | Gives every blood request a numeric priority (emergency vs. scheduled) |
| 📈 **Demand Forecasting** | Predicts future demand per blood type and region and raises early warnings |
| 🧪 **Verified Health Profile** | Partner labs update results directly, so no self-reported medical data |
| 🩺 **Doctor Final Approval** | AI assists, the doctor decides |
| 🔔 **Targeted Notifications** | Only suitable donors are notified for each request |
| 🛡️ **Fraud / Fake Request Detection** | Anomaly detection for duplicate or suspicious requests |
| 🔐 **Role-Based Access Control** | Sensitive medical data is visible only to authorized roles |

## 👥 User Roles

| Role | Interface | Main capabilities |
|---|---|---|
| **User** (Donor / Recipient) | Web / Mobile | Register, request blood, respond to matches, track donation history |
| **Hospital / Blood Bank** | Hospital Dashboard | Create requests, manage inventory, confirm donations |
| **Doctor** | Doctor Dashboard | Screen donors, review health profiles, give final approval |
| **Lab Partner** | Lab Dashboard | Upload and update verified test results |
| **Admin** | Admin Dashboard | Manage users, monitor fraud alerts, view analytics |

## 🔄 How It Works

```
User → Register/Login → Health Verification (Lab)
     → Request / Donor Registration
     → AI Engine (Validation → Urgency → Matching → Ranking)
     → Notification → Donor Response
     → Doctor Screening → Donation
     → Records Update → Better Future Predictions
```

## 🧱 Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React.js (Vite) |
| **Backend** | Python, FastAPI |
| **ORM** | SQLAlchemy 2.x + Alembic (migrations) |
| **Database** | PostgreSQL (SQL) |
| **Auth** | JWT + bcrypt, role-based access (RBAC) |
| **AI / ML** | Scikit-learn, XGBoost / LightGBM (separate microservice) |
| **Deployment** | Railway / Render (MVP) |

## 🗂️ Repository Structure

```
wasla/
├── backend/                 # FastAPI application
│   ├── app/
│   │   ├── main.py          # App entry point
│   │   ├── core/            # Config, security (JWT, hashing)
│   │   ├── db/              # SQLAlchemy engine, session, Base
│   │   ├── models/          # SQLAlchemy models (tables)
│   │   ├── schemas/         # Pydantic schemas (request/response)
│   │   ├── api/v1/          # Routers (auth, requests, donations, ...)
│   │   └── services/        # Business logic + AI Engine client
│   ├── alembic/             # DB migrations
│   ├── requirements.txt
│   └── .env.example
├── frontend/                # React application
│   ├── src/
│   └── .env.example
├── ai-engine/               # ML models & AI microservice
├── docs/                    # Specification, ERD, diagrams
├── assets/                  # Logo and images
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- **Python** 3.11+
- **Node.js** 18+ and npm
- **PostgreSQL** 14+ (or Docker)
- **Git**

### 1. Clone the repository

```bash
git clone https://github.com/<your-org>/wasla.git
cd wasla
```

### 2. Database (PostgreSQL)

Quick option using Docker:

```bash
docker run --name wasla-db \
  -e POSTGRES_USER=wasla \
  -e POSTGRES_PASSWORD=wasla_pass \
  -e POSTGRES_DB=wasla \
  -p 5432:5432 -d postgres:16
```

### 3. Backend (FastAPI)

```bash
cd backend

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env

# Run database migrations
alembic upgrade head

# Start the server
uvicorn app.main:app --reload
```

- API: http://localhost:8000
- Interactive docs (Swagger): http://localhost:8000/docs

**`backend/.env.example`**

```env
DATABASE_URL=postgresql+psycopg2://wasla:wasla_pass@localhost:5432/wasla
SECRET_KEY=change-me-to-a-long-random-string
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
AI_ENGINE_URL=http://localhost:8001
CORS_ORIGINS=http://localhost:5173
```

**Suggested `requirements.txt`**

```txt
fastapi
uvicorn[standard]
sqlalchemy>=2.0
alembic
psycopg2-binary
pydantic-settings
python-jose[cryptography]
passlib[bcrypt]
python-multipart
email-validator
httpx
pytest
```

### 4. Frontend (React)

```bash
cd frontend
npm install
cp .env.example .env
npm run dev
```

- App: http://localhost:5173

**`frontend/.env.example`**

```env
VITE_API_URL=http://localhost:8000/api
```

### 5. AI Engine (optional in early stages)

```bash
cd ai-engine
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --port 8001 --reload
```

> The backend must keep working with a **manual fallback** if the AI Engine is down: hospitals and doctors can always create and process requests manually.

## 🔌 Core API Endpoints

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| POST | `/api/auth/register` | Register a new user | No |
| POST | `/api/auth/login` | Login and receive JWT | No |
| POST | `/api/requests` | Create a blood request | Hospital |
| GET | `/api/requests/{id}/matches` | Ranked donor list | Hospital / Doctor |
| POST | `/api/donations/{id}/respond` | Donor accepts / declines | Donor |
| PUT | `/api/healthprofiles/{id}` | Update lab results | Lab |
| POST | `/api/donations/{id}/confirm` | Confirm completed donation | Hospital |

Full interactive documentation is available at `/docs` when the backend is running.

## 🗃️ Database

Managed with **SQLAlchemy** models and **Alembic** migrations.

Core entities: `Users`, `Donors`, `Hospitals`, `Doctors`, `Labs`, `BloodRequests`, `Donations`, `BloodInventory`, `HealthProfiles`, `LabResults`, `Notifications`, `AIRecommendations`, `RiskAlerts`.

Working with migrations:

```bash
# After changing a model
alembic revision --autogenerate -m "describe your change"
alembic upgrade head

# Roll back one step
alembic downgrade -1
```

## 🔐 Security & Privacy

- Role-Based Access Control on every endpoint
- Password hashing with bcrypt, JWT authentication
- Input validation with Pydantic
- Audit and access logs for any health-data interaction
- Explicit user consent before sharing health data
- Designed with Egypt's Personal Data Protection Law (No. 151 of 2020) in mind

## 🤝 Contributing

We follow a simple Git workflow:

1. Never push directly to `main`. Work on a branch: `feature/<name>`, `fix/<name>`, or `docs/<name>`.
2. Write clear commit messages, e.g. `feat(auth): add JWT login endpoint`.
3. Open a **Pull Request** and get at least **one review** before merging.
4. Keep PRs small and focused. Run tests before opening one.

```bash
git checkout -b feature/blood-request-api
git add .
git commit -m "feat(requests): add create blood request endpoint"
git push origin feature/blood-request-api
```

## 🧑‍🤝‍🧑 Team

| Member | Area |
|---|---|
| **Seif** | Backend Development (FastAPI, Auth, RBAC) |
| **Martin** | AI / ML Engineering |
| **Bejad** | Database & System Architecture |
| **Malak** | Frontend / Web Development |
| **Mariam** | UI/UX & Mobile Design |
| **Heaven** | Testing, Documentation & DevOps |

## 🗺️ Roadmap

- [x] Requirements & system design
- [ ] Database schema and migrations
- [ ] Core APIs and authentication
- [ ] AI Matching & Urgency Scoring (v1)
- [ ] User and Hospital dashboards
- [ ] Forecasting and Fraud Detection (v2)
- [ ] Testing and evaluation
- [ ] MVP deployment
- [ ] Final documentation and presentation

## ⚠️ Disclaimer

WASLA is an academic graduation project. AI in WASLA only **assists** with ranking, prediction, and alerts. It does **not** diagnose patients or replace medical judgment, and the final decision always belongs to the doctor. Training data in the prototype is synthetic.

---

<div align="center">

Made with ❤️ by the WASLA Team

</div>
