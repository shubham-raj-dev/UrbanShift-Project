# System Architecture

UrbanShift follows a decoupled Client-Server architecture.

## Overview
```mermaid
graph LR
    A[React Frontend (Vercel)] <-->|HTTP/REST| B(Django REST API)
    A <-->|WebSockets| C(Django Channels)
    B --> D[(Neon PostgreSQL)]
    C --> E[(Redis)]
    B --> F[Cloudinary]
```

## Frontend (Vercel)
- React serves as a Single Page Application (SPA).
- Communicates with the backend using Axios/Fetch for REST endpoints.
- Maintains WebSocket connections using standard Web APIs for the chat interface.

## Backend (Render)
- **WSGI**: Standard synchronous requests are handled by Gunicorn/Waitress (in dev) or Daphne.
- **ASGI (Daphne)**: Daphne is the primary server handling both HTTP and WebSocket traffic. 
- When a WebSocket connection is initiated, Django Channels takes over and routes the message through the Redis channel layer.

## Database (Neon)
- A serverless PostgreSQL instance hosted on Neon.tech.
- Connected via `dj_database_url` in Django settings.
- Highly available and separates compute from storage for cost-efficiency.

## Media Delivery (Cloudinary)
- Images uploaded by users (Property photos, Verification Docs, Profile Pics) are directly processed by Django and uploaded to Cloudinary.
- Cloudinary acts as a CDN, returning optimized URLs that are saved in the Neon database.
