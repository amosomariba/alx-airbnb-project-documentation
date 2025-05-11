

## 📝 `requirements.md`

**Project:** ALX Airbnb Backend
**Description:** Technical and Functional Requirements for Core Features

---

### 1. 🔐 User Authentication

#### Functional Requirements

* Users can register with a unique email and secure password.
* Users can log in with email and password to receive a token.
* Only authenticated users can access protected resources.

#### API Endpoints

| Method | Endpoint        | Description                           |
| ------ | --------------- | ------------------------------------- |
| POST   | `/api/register` | Register a new user                   |
| POST   | `/api/login`    | Authenticate user                     |
| GET    | `/api/profile`  | Retrieve user profile (auth required) |

#### Input/Output Specifications

**POST /api/register**

* Input: `first_name`, `last_name`, `email`, `password`
* Output: JSON response with user info or error

**POST /api/login**

* Input: `email`, `password`
* Output: Auth token on success or error

#### Validation Rules

* Email must be unique and in valid format
* Password must be 8+ characters
* All fields are required

#### Performance Criteria

* Auth token generation should be under 500ms
* Token should expire after 24 hours (JWT recommended)

---

### 2. 🏠 Property Management

#### Functional Requirements

* Hosts can create, update, and delete properties.
* All users can view property listings.
* Each property is tied to a host (user).

#### API Endpoints

| Method | Endpoint              | Description                     |
| ------ | --------------------- | ------------------------------- |
| GET    | `/api/properties`     | List all properties             |
| POST   | `/api/properties`     | Create new property (host only) |
| GET    | `/api/properties/:id` | Retrieve property details       |
| PUT    | `/api/properties/:id` | Update a property (host only)   |
| DELETE | `/api/properties/:id` | Delete a property (host only)   |

#### Input/Output Specifications

**POST /api/properties**

* Input: `name`, `description`, `location`, `pricepernight`
* Output: Property ID and confirmation message

#### Validation Rules

* All fields are required except `updated_at`
* `pricepernight` must be a decimal > 0

#### Performance Criteria

* Response to create/update should be under 1s
* Listing retrieval should be paginated (default: 10 per page)

---

### 3. 📅 Booking System

#### Functional Requirements

* Guests can book properties for specific dates.
* System must check for availability and calculate total cost.
* Guests can view and cancel their bookings.

#### API Endpoints

| Method | Endpoint            | Description                |
| ------ | ------------------- | -------------------------- |
| POST   | `/api/bookings`     | Create new booking         |
| GET    | `/api/bookings`     | List all bookings for user |
| PUT    | `/api/bookings/:id` | Update booking (optional)  |
| DELETE | `/api/bookings/:id` | Cancel booking             |

#### Input/Output Specifications

**POST /api/bookings**

* Input: `property_id`, `start_date`, `end_date`
* Output: Booking ID, total price, status (pending)

#### Validation Rules

* `start_date` < `end_date`
* No overlapping bookings allowed
* Booking dates must be in the future

#### Performance Criteria

* Availability check must be instant (<1s)
* Max 100 bookings should be retrieved efficiently with pagination

---

