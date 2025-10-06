# 🧩 FitMate App – Technical Specification Document

## 📘 Overview
**FitMate** adalah aplikasi mobile berbasis **Flutter** dengan backend **Laravel** dan database **PostgreSQL**, dirancang untuk membantu pengguna menjaga gaya hidup sehat melalui fitur **AI Chat**, **Food Scanner**, **Gym Finder**, dan **Health News**.

Aplikasi ini dikembangkan menggunakan metodologi **Agile Scrum** dengan fase sprint dan CI/CD pipeline untuk memastikan integrasi dan deployment yang konsisten.

---

## ⚙️ Tech Stack Summary

| Layer | Technology | Description |
|-------|-------------|--------------|
| Frontend (Mobile) | Flutter 3.x | UI/UX interaktif, mendukung Android & iOS |
| Backend (API) | Laravel 11.x | RESTful API service dan business logic |
| Database | PostgreSQL 15+ | Penyimpanan data relasional dan JSON |
| AI Service | Google Gemini API | Natural language & recommendation model |
| Cloud Infra | Railway / Render | Deployment dan auto-scaling |
| Auth & Notification | Firebase | Authentication & Push Notification |
| Payment | Midtrans / Xendit | Subscription & payment gateway |
| Storage | Firebase Storage / S3 | Media & image asset management |
| Version Control | GitHub | Repository & issue tracking |
| CI/CD | GitHub Actions | Automated testing & deployment |
| API Security | JWT + HTTPS | Token-based auth & TLS encryption |

---

## 🧱 System Architecture Overview

![System Architecture Diagram](A_system_architecture_diagram_in_digital_vector_gr.png)

### 🔍 Penjelasan Komponen:
- **User (Flutter App)** → berinteraksi dengan fitur AI, pemindaian makanan, berita, dan gym finder.
- **Laravel API Gateway** → menangani permintaan dari aplikasi mobile dan berinteraksi dengan database.
- **PostgreSQL Database** → menyimpan data pengguna, makanan, dan histori chat AI.
- **AI Service (Gemini API)** → memberikan rekomendasi personal terkait olahraga dan nutrisi.
- **Firebase Auth & Storage** → mengelola login, signup, dan penyimpanan gambar pengguna.
- **Midtrans/Xendit Payment Gateway** → memproses transaksi langganan fitur premium.
- **GitHub Actions (CI/CD)** → otomatisasi build, test, dan deployment ke Railway Cloud.

---

## 📁 Repository Setup

### 1. Struktur GitHub
fitmate/
├── frontend/ (Flutter)
├── backend/ (Laravel)
├── docs/ (Documentation)
└── .github/workflows/ (CI/CD pipeline)

yaml
Copy code

### 2. Branching Workflow
| Branch | Purpose |
|---------|----------|
| `main` | Production-ready code |
| `develop` | Active development branch |
| `feature/*` | New feature development |
| `bugfix/*` | Hotfix atau perbaikan bug |
| `release/*` | Pre-production stabilization |

---

## 🧪 Development Environment Setup

### 🔧 Backend (Laravel)
```bash
git clone https://github.com/haykalaul/fitmate.git
cd backend
cp .env.example .env
composer install
php artisan key:generate
php artisan migrate --seed
php artisan serve
🧠 Frontend (Flutter)
bash
Copy code
cd frontend
flutter pub get
flutter run
🔌 Database
Pastikan PostgreSQL berjalan:

bash
Copy code
psql -U postgres -d fitmate_db
Struktur dasar tabel:

users

foods

exercises

subscriptions

chat_histories

api_logs

🔐 Security Specification
JWT Authentication untuk API access.

HTTPS enforced via Railway/Render.

Input sanitization (Laravel Request Validation).

Role-based access control (Admin, User, QA Tester).

API rate limiting.

🚀 Deployment Process
CI/CD Pipeline (GitHub Actions)
Trigger: push ke main atau release/*

Steps:

Install dependencies (composer, npm, flutter)

Run unit & integration tests

Build production artifact

Deploy to Railway/Render via API key

yaml
Copy code
# .github/workflows/deploy.yml
on:
  push:
    branches: [ main ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.3'
      - name: Install Dependencies
        run: composer install --no-dev
      - name: Deploy
        run: curl -X POST ${{ secrets.RAILWAY_DEPLOY_HOOK }}
## 🧩 API Overview
Endpoint	Method	Description	Auth
/api/login	POST	Login user	No
/api/register	POST	Register user	No
/api/foods/scan	POST	Upload food image & analyze calories	Yes
/api/chat/ai	POST	Chat with AI trainer	Yes
/api/news	GET	Fetch latest health news	No
/api/gyms/nearby	GET	Find nearby gyms	Yes
/api/payment/subscribe	POST	Initiate subscription payment	Yes

## 🧠 Testing Strategy
Unit Test: Laravel PHPUnit, Flutter test

Integration Test: Postman/Newman API suite

UAT: Simulasi pengguna akhir dengan feedback QA

Load Test: Apache Benchmark (target <3s response @1000 users)

## 🧭 Versioning
Menggunakan Semantic Versioning (SemVer):

makefile
Copy code
MAJOR.MINOR.PATCH
contoh: v1.2.0
🧑‍💻 Maintainers
Role	Name	Responsibility
Project Manager	—	Pengawasan keseluruhan proyek
Business Analyst	—	Analisis kebutuhan & SRS
UI/UX Designer	—	Wireframe, Mockup, Prototype
Backend Dev	—	API & Database
Frontend Dev	—	Flutter App
QA Tester	—	Testing & Bug Report

##🏁 Deployment Checklist
 Database migrated dan seeded

 Firebase & API key dikonfigurasi

 SSL aktif di domain

 CI/CD pipeline sukses

 Play Store Beta release

 Post-release monitoring aktif

