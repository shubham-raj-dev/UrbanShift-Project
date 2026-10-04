# Deployment Guide

## Backend Deployment (Render)

1. **Platform**: Render.com Web Service.
2. **Environment**: Python 3.
3. **Build Command**: `pip install -r requirements.txt && python manage.py migrate`
4. **Start Command**: `daphne -b 0.0.0.0 -p 8000 backend.asgi:application`
5. **Environment Variables Required**:
   - `DATABASE_URL` (Neon PostgreSQL URL)
   - `REDIS_URL` (Render Redis URL)
   - `SECRET_KEY`, `DEBUG` (False), `ALLOWED_HOSTS`
   - `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`
   - `BREVO_API_KEY`, `BREVO_SMTP_LOGIN`
   - `RAZORPAY_KEY_ID`, `RAZORPAY_KEY_SECRET`

## Frontend Deployment (Vercel)

1. **Platform**: Vercel.
2. **Framework Preset**: Create React App.
3. **Build Command**: `npm run build`
4. **Output Directory**: `build`
5. **Environment Variables Required**:
   - `REACT_APP_API_URL` (Point to Render backend URL)
   - `REACT_APP_FIREBASE_API_KEY` and other Firebase config variables.
   - `REACT_APP_RAZORPAY_KEY_ID`

## Troubleshooting
- If Render throws 429 Too Many Requests during health checks, ensure the `/health/` endpoint is exempted from caching/rate-limits.
- Websockets on Vercel: Vercel routes HTTP traffic. WebSocket connections go directly from the client's browser to the Render backend, bypassing Vercel.
