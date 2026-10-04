# Database Schema

The database uses PostgreSQL (hosted on Neon). Below is an overview of the core models and their relationships.

## Core Models

### User (Custom `AbstractUser`)
- Extends standard Django user.
- **Key Fields**: `user_type` (BUYER, SELLER, COMPANY), `phone_number`, `is_verified`, `profile_picture`.
- **Relations**: Properties listed (1:N), Properties purchased (1:N), Wishlist items (1:N).

### Property
- **Key Fields**: `title`, `description`, `price`, `location`, `category` (RENT/SELL), `bedrooms`, `is_sold`.
- **Relations**: 
  - `seller` (FK to User)
  - `buyer` (FK to User, nullable)

### PropertyImage
- **Key Fields**: `image_url`, `image` (FileField).
- **Relations**: `property` (FK to Property). Allows multiple images per property.

### Wishlist
- **Relations**: `user` (FK to User), `property` (FK to Property).
- Unique together constraint on (user, property).

### RelocationRequest (Packers & Movers)
- **Key Fields**: `pickup_address`, `dropoff_address`, `moving_date`, `status` (PENDING, ACCEPTED, REJECTED).
- **Relations**: 
  - `customer` (FK to User)
  - `company` (FK to User where user_type=COMPANY)

### ChatMessage
- **Key Fields**: `content`, `timestamp`, `is_read`.
- **Relations**: 
  - `sender` (FK to User)
  - `receiver` (FK to User)
