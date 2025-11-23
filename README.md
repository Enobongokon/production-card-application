# Production Card MVP - Complete System

A complete production card management system with Android mobile app, FastAPI backend, React admin portal, and MySQL database.

## System Overview

### Components
1. **Android Mobile App (Kotlin)** - For employees to view and submit production cards
2. **FastAPI Backend (Python)** - RESTful API server with authentication and business logic
3. **React Admin Portal** - Web interface for administrators
4. **MySQL Database** - Data persistence layer

### Key Features
- Phone + Password + SMS OTP authentication
- Device binding with hash (one device per user)
- Device rebind request workflow
- Root detection on Android
- Multi-language support (English, Tamil, Hindi)
- GPS-based geofencing (500m radius)
- Production card assignment and submission
- CSV data export
- Mobile-responsive admin portal

## Quick Start

### Option 1: Using Docker (Recommended)

```bash
# Start database and backend
docker-compose up -d

# Backend will be available at http://localhost:8000
# MySQL will be available at localhost:3306
```

### Option 2: Manual Setup

#### Backend Setup
```bash
cd backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your database credentials

# Run server
uvicorn app.main:app --reload
```

Backend will run on http://localhost:8000

#### Admin Portal Setup
```bash
cd admin

# Install dependencies
npm install

# Start development server
npm run dev
```

Admin portal will run on http://localhost:3000

#### Android App Setup
1. Open `android/` folder in Android Studio
2. Update `ApiService.kt` with your backend URL
3. Build and run on emulator or device

## Database Setup

### Using Docker
Database will be automatically created when running `docker-compose up`

### Manual MySQL Setup
```sql
CREATE DATABASE production_card_db;
```

Then run the FastAPI server - tables will be created automatically using SQLAlchemy.

For sample data, run: `backend/app/db/migrations/init_db.sql`

## Test Credentials

### Admin
- Phone: +919876543210
- Password: admin123

### Employees
- Phone: +919876543211 (Ravi Kumar)
- Phone: +919876543212 (Priya Sharma)
- Phone: +919876543213 (Arun Patel)
- Password: employee123

## API Documentation

Once the backend is running, visit:
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

## Architecture

See individual component READMEs:
- Backend: `backend/README.md`
- Admin Portal: `admin/README.md`
- Android App: `android/README.md`

## Security Features

### Device Binding
- Each user can only use one device
- Device identified by hashed Android ID
- Login on new device creates rebind request
- Admin approval required for device change

### Root Detection
- Checks for SU binaries
- Checks build tags
- Checks for root management apps
- Blocks access and alerts admin

### Geofencing
- Uses Haversine formula
- Validates submission within 500m of site
- Rejects submissions outside geofence

### Authentication
- JWT tokens with expiration
- Password hashing with bcrypt
- OTP verification for first login
- Admin role verification

## Deployment

### Backend (Docker)
```bash
cd backend
docker build -t production-card-api .
docker run -p 8000:8000 production-card-api
```

### Admin Portal
```bash
cd admin
npm run build
# Deploy dist/ folder to any static hosting (Netlify, Vercel, S3, etc.)
```

### Android App
Build release APK:
```bash
cd android
./gradlew assembleRelease
```

## Troubleshooting

### Backend Issues
- Check database connection in `.env`
- Ensure MySQL is running
- Check port 8000 is available

### Android Issues
- Update backend URL in `ApiService.kt`
- Use `10.0.2.2` for emulator
- Use actual IP for physical device
- Check location permissions

### Admin Portal Issues
- Update API URL in `src/api/index.js`
- Check CORS settings in backend
- Clear browser cache

## License

This is an MVP/prototype application for internal use.

