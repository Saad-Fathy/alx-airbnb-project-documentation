Airbnb Clone Backend Requirement Specifications
Overview
This document details the technical and functional requirements for three key features of the Airbnb Clone backend: User Authentication, Property Management, and Booking System. Each feature includes functional requirements, RESTful API endpoints, input/output specifications, validation rules, and performance criteria. The specifications align with the features from Task 0, use cases from Task 1, and the database schema, supporting the RESTful API design.
1. User Authentication
Functional Requirements

Allow users to register with email, password, and role (guest, host, admin, or both).
Authenticate users via email/password, issuing a JWT for secure access.
Support profile updates (e.g., phone number, password) and account deletion.
Store passwords securely using bcrypt.
Restrict actions based on user role.

API Endpoints
POST /users/register

Description: Register a new user.
Request:
Body (JSON):{
  "first_name": "string",
  "last_name": "string",
  "email": "string",
  "password": "string",
  "phone_number": "string" (optional),
  "role": "string" (enum: guest, host, admin, both)
}


Example:{
  "first_name": "Alice",
  "last_name": "Smith",
  "email": "alice.smith@example.com",
  "password": "Password123!",
  "phone_number": "+1-555-0101",
  "role": "host"
}




Response:
201 Created: { "user_id": "UUID", "message": "User registered successfully" }
400 Bad Request: { "error": "Invalid input" }
409 Conflict: { "error": "Email already registered" }


Validation Rules:
first_name, last_name: Required, string, 1–50 characters.
email: Required, valid email format, unique in Users table.
password: Required, string, 8–50 characters, must include uppercase, lowercase, number, special character.
phone_number: Optional, valid phone format.
role: Required, enum ['guest', 'host', 'admin', 'both'].



POST /users/login

Description: Authenticate a user and issue a JWT.
Request:
Body (JSON):{
  "email": "string",
  "password": "string"
}


Example:{
  "email": "alice.smith@example.com",
  "password": "Password123!"
}




Response:
200 OK: { "user_id": "UUID", "token": "JWT", "role": "string" }
401 Unauthorized: { "error": "Invalid credentials" }
400 Bad Request: { "error": "Missing email or password" }


Validation Rules:
email: Required, valid email format.
password: Required, string, 8–50 characters.



PUT /users/:id

Description: Update user profile.
Request:
Path: :id (UUID).
Headers: Authorization: Bearer 
Body (JSON):{
  "phone_number": "string" (optional),
  "password": "string" (optional)
}


Example:{
  "phone_number": "+1-555-0102",
  "password": "NewPassword123!"
}




Response:
200 OK: { "message": "Profile updated successfully" }
400 Bad Request: { "error": "Invalid input" }
401 Unauthorized: { "error": "Invalid token" }
403 Forbidden: { "error": "Unauthorized to update this user" }


Validation Rules:
:id: Valid UUID, matches authenticated user or admin.
phone_number: Optional, valid phone format.
password: Optional, 8–50 characters, meets complexity requirements.



Performance Criteria

Response Time: <500ms for registration/login under normal load.
Scalability: Handle 10,000 concurrent registration requests with <1% failure rate.
Reliability: 99.9% uptime for authentication endpoints.
Security: Passwords hashed with bcrypt, JWTs signed with HS256, tokens expire in 24 hours.

2. Property Management
Functional Requirements

Allow hosts to create, update, and delete property listings.
Enable users to view and search properties by criteria (e.g., location, price).
Restrict property modifications to the owning host or admins.
Link properties to valid locations and hosts.

API Endpoints
POST /properties

Description: Create a new property listing.
Request:
Headers: Authorization: Bearer  (host/admin role).
Body (JSON):{
  "name": "string",
  "description": "string",
  "location_id": "UUID",
  "pricepernight": "number"
}


Example:{
  "name": "Cozy NYC Loft",
  "description": "A stylish loft in downtown Manhattan.",
  "location_id": "550e8400-e29b-41d4-a716-446655440100",
  "pricepernight": 150.00
}




Response:
201 Created: { "property_id": "UUID", "message": "Property created successfully" }
400 Bad Request: { "error": "Invalid input" }
401 Unauthorized: { "error": "Invalid token" }
403 Forbidden: { "error": "Only hosts can create properties" }


Validation Rules:
name: Required, string


