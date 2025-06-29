# Backend Feature Requirements – ALX Airbnb Project

## 1. User Authentication

### Functional Requirements
- Users must be able to register, log in, and log out securely.
- Passwords must be stored using encryption.
- Only authenticated users can access protected endpoints.

### API Endpoints
| Method | Endpoint         | Description            |
|--------|------------------|------------------------|
| POST   | /api/register    | Register new user      |
| POST   | /api/login       | Authenticate user      |
| POST   | /api/logout      | Log out current user   |

### Input/Output Specification
- **/api/register**
  - **Input**: JSON `{ "email": "user@example.com", "password": "SecurePass123" }`
  - **Output**: `201 Created`, user ID or error message

- **/api/login**
  - **Input**: JSON `{ "email": "user@example.com", "password": "SecurePass123" }`
  - **Output**: `200 OK`, auth token or error

### Validation Rules
- Email must be unique and valid format.
- Password must be at least 8 characters.
  
### Performance Criteria
- Registration and login should respond in under 500ms.
- Auth token should expire after a set period (e.g., 24 hours).

---

## 2. Property Management

### Functional Requirements
- Hosts can create, update, and delete properties.
- Guests can browse and view property details.
- Each property must have location, price, and availability info.

### API Endpoints
| Method | Endpoint             | Description            |
|--------|----------------------|------------------------|
| POST   | /api/properties      | Create property        |
| GET    | /api/properties      | List all properties    |
| GET    | /api/properties/:id  | View single property   |
| PUT    | /api/properties/:id  | Update property        |
| DELETE | /api/properties/:id  | Delete property        |

### Input/Output Specification
- **POST /api/properties**
  - **Input**: JSON with property fields (title, description, price, etc.)
  - **Output**: `201 Created`, property ID

### Validation Rules
- Title and location are required.
- Price must be a positive number.

### Performance Criteria
- Properties list should paginate (e.g., 20 per page).
- Max response time: 700ms for listing.

---

## 3. Booking System

### Functional Requirements
- Logged-in users can book available properties.
- System prevents double bookings for the same dates.

### API Endpoints
| Method | Endpoint             | Description         |
|--------|----------------------|---------------------|
| POST   | /api/bookings        | Create booking      |
| GET    | /api/bookings        | Get user bookings   |

### Input/Output Specification
- **POST /api/bookings**
  - **Input**: JSON `{ "property_id": 123, "start_date": "2025-07-01", "end_date": "2025-07-05" }`
  - **Output**: `201 Created`, booking ID or error

### Validation Rules
- Booking dates must be in the future.
- End date must be after start date.
- No overlapping bookings.

### Performance Criteria
- Booking checks (availability + creation) must complete in under 1 second.

