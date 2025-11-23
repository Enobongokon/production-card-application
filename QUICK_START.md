# Quick Start Guide

## Prerequisites
- Python 3.11+
- Node.js 18+
- MySQL 8.0 or Docker
- Android Studio (for mobile app)

## 1. Start Backend

```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

Visit: http://localhost:8000/docs

## 2. Start Admin Portal

```bash
cd admin
npm install
npm run dev
```

Visit: http://localhost:3000

## 3. Setup Android App

1. Open `android/` in Android Studio
2. Edit `services/ApiService.kt`:
   ```kotlin
   private const val BASE_URL = "http://10.0.2.2:8000/"  // For emulator
   ```
3. Build and run

## 4. Test the System

### Login as Admin
- Open http://localhost:3000
- Phone: +919876543210
- Password: admin123

### Login as Employee (Android)
- Phone: +919876543211
- Password: employee123
- Enter OTP shown in backend console

## Next Steps
- Assign production cards to employees
- Submit cards with GPS location
- View submissions in admin portal
- Export data as CSV

