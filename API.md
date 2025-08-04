# REST API Endpoints for Booking System

## 🔐 User & Role Management

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Register               | POST   | `/api/auth/register`          | Create new user account              |
| Login                  | POST   | `/api/auth/login`             | Authenticate user                    |
| Get current user       | GET    | `/api/users/me`               | Get logged-in user data              |
| Update profile         | PATCH  | `/api/users/me`               | Edit user name, phone, email         |
| Get all roles          | GET    | `/api/roles`                  | Admin only – list all roles          |
| Assign user role       | POST   | `/api/users/:userId/roles`    | Admin – assign role to user          |
| Get user's roles       | GET    | `/api/users/:userId/roles`    | Admin – view user's assigned roles   |

---

## 🌍 Cities & Airports

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| List cities            | GET    | `/api/cities`                 | Get all cities                       |
| Create city            | POST   | `/api/cities`                 | Admin – Add new city                 |
| List airports          | GET    | `/api/airports`               | Get all airports                     |
| Create airport         | POST   | `/api/airports`               | Admin – Add new airport              |
| Get airport by ID      | GET    | `/api/airports/:id`           | View airport details                 |

---

## ✈️ Flights

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Search flights         | GET    | `/api/flights/search`         | Query params: `from`, `to`, `date`   |
| Get all flights        | GET    | `/api/flights`                | List available flights               |
| Get flight details     | GET    | `/api/flights/:flightId`      | Detailed view                        |
| Create flight          | POST   | `/api/flights`                | Admin only – add a flight            |
| Update flight          | PATCH  | `/api/flights/:flightId`      | Admin – edit flight                  |
| Delete flight          | DELETE | `/api/flights/:flightId`      | Admin – remove flight                |

---

## 🏨 Hotels & Rooms

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| List hotels            | GET    | `/api/hotels`                 | Browse hotels                        |
| Get hotel by ID        | GET    | `/api/hotels/:hotelId`        | View hotel details                   |
| Create hotel           | POST   | `/api/hotels`                 | Admin – add hotel                    |
| List rooms             | GET    | `/api/hotels/:hotelId/rooms`  | Rooms within a hotel                 |
| Get room details       | GET    | `/api/rooms/:roomId`          | View room                            |
| Create room            | POST   | `/api/hotels/:hotelId/rooms`  | Admin – add room                     |
| Update room            | PATCH  | `/api/rooms/:roomId`          | Admin – update room                  |

---

## 📦 Bookings

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Create booking         | POST   | `/api/bookings`               | Create new booking                   |
| Add item to booking    | POST   | `/api/bookings/:id/items`     | Add flight/hotel to booking          |
| View booking           | GET    | `/api/bookings/:id`           | View full booking + items            |
| Cancel booking         | PATCH  | `/api/bookings/:id/cancel`    | Cancel booking                       |
| List my bookings       | GET    | `/api/bookings`               | Get user's bookings                  |
| List all bookings      | GET    | `/api/admin/bookings`         | Admin – all bookings                 |

---

## 💳 Payments

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Make payment           | POST   | `/api/payments`               | Pay for a booking                    |
| Get payment by ID      | GET    | `/api/payments/:id`           | View payment details                 |
| List all payments      | GET    | `/api/admin/payments`         | Admin – all payment logs             |

---

## ⭐ Favorites

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Add favorite           | POST   | `/api/favorites`              | Add flight/room to favorites         |
| List my favorites      | GET    | `/api/favorites`              | Get current user’s favorites         |
| Remove favorite        | DELETE | `/api/favorites/:favoriteId`  | Remove from favorites                |

---

## 🧳 Saved Trips

| Action                 | Method | Endpoint                      | Description                          |
|------------------------|--------|-------------------------------|--------------------------------------|
| Save a trip plan       | POST   | `/api/trips`                  | Save flight + hotel bundle           |
| List my saved trips    | GET    | `/api/trips`                  | Retrieve saved trips                 |
| View trip              | GET    | `/api/trips/:tripId`          | Trip details                         |
| Delete trip            | DELETE | `/api/trips/:tripId`          | Remove saved trip                    |

---

### Notes

- **Admin endpoints** require `role=Admin` in the user's JWT token.
- **Authentication**: All endpoints (except `/auth/register` and `/auth/login`) require a valid JWT in the `Authorization` header.
- **Error Responses**: Standard HTTP status codes (4xx for client errors, 5xx for server errors).
