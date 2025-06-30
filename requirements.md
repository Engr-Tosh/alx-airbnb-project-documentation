# Airbnb Clone Backend Feature Specifications

## 1. User Authentication

### Functional Requirements:
- Users must be able to register and log in as a Guest or Host.
- Authentication should use JWT for session management.
- OAuth (e.g., Google login) should be supported.
- Users must be able to update profile information.

### Technical Requirements:
- **API Endpoints:**
  - `POST /api/auth/register`
  - `POST /api/auth/login`
  - `GET /api/auth/profile`
  - `PUT /api/auth/profile`

### Input Specifications:
- **Register:** `email`, `password`, `role` (guest/host), `name`
- **Login:** `email`, `password`
- **Update Profile:** `name`, `profilePhoto`, `phoneNumber`

### Output Specifications:
- JWT access token
- Profile JSON object

### Validation Rules:
- Email must be valid and unique.
- Password must be at least 8 characters.
- Role must be either `guest` or `host`.

### Performance Criteria:
- Token generation must occur under 200ms.
- Profile fetch must return within 300ms.

---

## 2. Property Management

### Functional Requirements:
- Hosts must be able to create, edit, and delete listings.
- Listings must include title, description, location, price, and amenities.
- Listings must support multiple images.

### Technical Requirements:
- **API Endpoints:**
  - `POST /api/properties`
  - `GET /api/properties/:id`
  - `PUT /api/properties/:id`
  - `DELETE /api/properties/:id`
  - `GET /api/properties?filters`

### Input Specifications:
- `title`, `description`, `location`, `price`, `amenities`, `availabilityDates`, `images[]`

### Output Specifications:
- JSON listing object

### Validation Rules:
- Title and location are required.
- Price must be a positive number.
- Maximum of 10 images per listing.

### Performance Criteria:
- Search with filters must return within 500ms.
- Image uploads must complete within 3 seconds.

---

## 3. Booking System

### Functional Requirements:
- Guests must be able to book properties for specific dates.
- System must prevent overlapping bookings.
- Guests and hosts must be able to cancel bookings.

### Technical Requirements:
- **API Endpoints:**
  - `POST /api/bookings`
  - `GET /api/bookings/:id`
  - `GET /api/bookings?userId=`
  - `DELETE /api/bookings/:id`

### Input Specifications:
- `userId`, `propertyId`, `startDate`, `endDate`, `guests`

### Output Specifications:
- JSON booking object

### Validation Rules:
- Booking dates must not overlap with existing bookings.
- Start date must be before end date.
- Maximum stay length = 30 days.

### Performance Criteria:
- Booking confirmation response within 500ms.
- Cancellation should update availability in real-time.
