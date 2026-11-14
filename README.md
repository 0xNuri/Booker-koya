# Koya's Clinic Booking API

A booking API for a clinic that lets patients view available appointment slots, make bookings, and manage them. Includes a simple web interface.

## Features

| Level | Capabilities |
|-------|--------------|
| 1 | Listing slots, booking slots, looking up a booking |
| 2 | API key authentication, input validation |
| 3 | Concurrency-safe bookings, cancellation |
| 4 | Idempotent requests, cursor-based pagination |
| 5 | Per-email rate limiting (5 requests/minute) |

## Tech Stack

- **Runtime**: Node.js (ESM)
- **Framework**: Express v5
- **Database**: PostgreSQL
- **Frontend**: Vanilla HTML/CSS/JS

## API Reference

Full OpenAPI spec: [koyaacademy.com/assessment-api](https://koyaacademy.com/assessment-api)

Every API request requires the `X-API-Key` header.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/reset` | Replace all slots |
| `GET` | `/slots` | List all slots |
| `POST` | `/bookings` | Book a slot |
| `GET` | `/bookings` | List bookings (paginated) |
| `GET` | `/bookings/:id` | Get a booking |
| `DELETE` | `/bookings/:id` | Cancel a booking |

## Running Locally

1. **Clone the repo**

   ```bash
   git clone https://github.com/0xnuri/booker-koya.git
   cd booker-koya
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Create a `.env` file in the project root**

   ```env
   DATABASE_URL=postgres://your_db_url
   API_KEY=your_secret_key
   PORT=3000
   ```

4. **Start the server**

   ```bash
   npm start
   ```

The app runs on http://localhost:3000.

## Project Structure

```text
├── index.js                      # App entry point
├── public/
│   └── index.html                # Web interface
└── src/
    ├── models/
    │   ├── migrations.js         # DB schema setup
    │   ├── seedSlots.js          # Initial slot seeder
    │   ├── pool.js               # Postgres connection pool
    │   ├── slotRepository.js     # Slot DB queries
    │   ├── bookingRepositiory.js # Booking DB queries
    │   └── idempotencyRepository.js # Idempotency DB queries
    ├── services/
    │   ├── booker.js             # Business logic
    │   └── idempSet.js           # Idempotency logic
    ├── routes/
    │   └── routes.js             # Express route handlers
    └── utils/
        └── rateLimiter.js        # Sliding window rate limiter
```