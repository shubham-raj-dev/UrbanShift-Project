# API Documentation

The UrbanShift backend exposes RESTful API endpoints via Django REST Framework (DRF).

## Base URL
`/api/`

## Authentication
Authentication is handled via JWT (JSON Web Tokens). Most protected endpoints require the `Authorization: Bearer <token>` header.

### Endpoints

#### Users (`/api/users/`)
- `POST /register/`: Register a new user (Buyer, Seller, Company).
- `POST /login/`: Obtain JWT access and refresh tokens.
- `POST /google-auth/`: Authenticate using Firebase Google Auth token.
- `GET /profile/`: Fetch current user details.

#### Properties (`/api/properties/`)
- `GET /`: List all properties.
- `POST /`: Create a new property (Seller only).
- `GET /<id>/`: Retrieve specific property details.
- `POST /<id>/wishlist/`: Toggle property in the user's wishlist.

#### Relocation (`/api/relocation/`)
- `GET /companies/`: List all Packers & Movers companies.
- `POST /book/`: Submit a moving request to a specific company.
- `GET /my-requests/`: See status of submitted requests.

#### Chat (`/api/chat/`)
- `GET /history/<user_id>/`: Retrieve chat message history with a specific user.

## WebSockets (Real-time Chat)
- **URL**: `ws://<backend-domain>/ws/chat/<room_name>/`
- Handles real-time messaging between users. Requires authentication via query parameters or session headers.
