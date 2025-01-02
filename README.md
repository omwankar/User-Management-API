# User Management API Documentation

This API allows for user registration, login, and profile management with JWT-based authentication.

## Base URL

The API is hosted at `http://localhost:3000` by default.

---

## Authentication

JWT (JSON Web Token) is used for authentication. To access certain endpoints (e.g., user profile), you must include a valid JWT token in the `Authorization` header.

### Example Authorization Header:
```bash
Authorization: Bearer <your_jwt_token>
Endpoints
1. Register a New User
URL: /register
Method: POST
Description: Registers a new user.
Request Body:
json
Copy code
{
  "username": "johndoe",
  "email": "johndoe@example.com",
  "password": "password123"
}
Responses:
201: User created successfully
400: Invalid input
json
Copy code
{
  "message": "User created successfully.",
  "user": {
    "username": "johndoe",
    "email": "johndoe@example.com",
    "password": "<hashed_password>"
  }
}
2. Login User
URL: /login
Method: POST
Description: Logs in a user and returns a JWT token.
Request Body:
json
Copy code
{
  "email": "johndoe@example.com",
  "password": "password123"
}
Responses:
200: Login successful, returns a JWT token.
json
Copy code
{
  "token": "<jwt_token>"
}
401: Invalid credentials
3. Get User Profile
URL: /profile
Method: GET
Description: Retrieves the profile information of the authenticated user.
Authentication: Requires a valid JWT token.
Responses:
200: User profile retrieved
json
Copy code
{
  "username": "johndoe",
  "email": "johndoe@example.com"
}
401: Unauthorized
4. Update User Profile (Optional)
URL: /profile
Method: PUT
Description: Updates the profile information of the authenticated user.
Authentication: Requires a valid JWT token.
Request Body:
json
Copy code
{
  "username": "newusername",
  "email": "newemail@example.com"
}
Responses:
200: Profile updated successfully
400: Invalid input
401: Unauthorized
5. Delete User Profile (Optional)
URL: /profile
Method: DELETE
Description: Deletes the authenticated user's profile.
Authentication: Requires a valid JWT token.
Responses:
200: Profile deleted successfully
401: Unauthorized
Error Codes
400: Bad Request (e.g., missing required fields)
401: Unauthorized (e.g., missing or invalid token)
404: Not Found (e.g., user not found)
500: Internal Server Error (e.g., unexpected server issues)
Example Requests
Register a New User
bash
Copy code
curl -X POST http://localhost:3000/register -H "Content-Type: application/json" -d '{"username": "johndoe", "email": "johndoe@example.com", "password": "password123"}'
Login
bash
Copy code
curl -X POST http://localhost:3000/login -H "Content-Type: application/json" -d '{"email": "johndoe@example.com", "password": "password123"}'
Get User Profile
bash
Copy code
curl -X GET http://localhost:3000/profile -H "Authorization: Bearer <your_jwt_token>"
