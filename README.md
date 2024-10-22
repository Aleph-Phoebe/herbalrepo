### Herbal Remedy Web App - Backend
### Project Overview
The Herbal Remedy Web App provides users with natural alternatives to conventional medicine by offering a searchable database of herbal remedies. Users can:

Sign up and log in securely.
Add remedies to their favorites list.
Review and rate the effectiveness of remedies.
Search remedies by symptoms, ingredients, or remedy type.
This documentation provides a comprehensive guide for setting up and using the backend API for this application.

### Features
User Authentication: Secure registration, login, and profile management.
Remedy Database: Add, retrieve, and manage herbal remedies.
Favorites: Users can save remedies as favorites.
Reviews & Ratings: Users can review and rate remedies they’ve tried.
Search Functionality: Search for remedies based on symptoms or ingredients.
Technologies Used
Python & Flask: Backend framework for API development.
PostgreSQL: Relational database for storing remedies, users, and reviews.
SQLAlchemy: ORM for interacting with the PostgreSQL database.
Flask-Migrate: For database migrations.
JWT: JSON Web Tokens for secure user authentication.
Postman: API endpoint testing during development.

### Project Setup:
Clone the repository:
bash
git clone <repository-url>
cd folder

Install dependencies:
bash
pip install -r requirements.txt
Set up environment variables:

Create a .env file in the root directory with the following keys:
bash
SECRET_KEY=your_secret_key
DATABASE_URL=postgresql://username:password@localhost/herbal_db
JWT_SECRET_KEY=your_jwt_secret_key

Set up the database:

Ensure PostgreSQL is installed and running.
Create the database:
bash
psql
CREATE DATABASE herbal_db;
Run migrations to apply the database schema:

bash
flask db upgrade

Run the application:

bash
flask run

Environment Variables
SECRET_KEY: Used to sign session data securely.
DATABASE_URL: Connection string to your PostgreSQL database.
JWT_SECRET_KEY: Secret key for signing JWT tokens.
Database Models
The project uses four main models:

User Model

Fields:
id: Integer (Primary Key)
username: String (Unique username)
email: String (Unique email)
password_hash: String (Hashed password)
Remedy Model

Fields:
id: Integer (Primary Key)
name: String (Remedy name)
ingredients: String (List of ingredients)
symptoms: String (Related symptoms)
user_id: Integer (Foreign key to User)
Favorite Model

Fields:
id: Integer (Primary Key)
user_id: Integer (Foreign key to User)
remedy_id: Integer (Foreign key to Remedy)
Review Model

Fields:
id: Integer (Primary Key)
user_id: Integer (Foreign key to User)
remedy_id: Integer (Foreign key to Remedy)
rating: Integer (Rating value from 1 to 5)
comment: String (Review comment)
API Endpoints
Authentication Routes
Sign Up

Endpoint: /api/signup
Method: POST
Description: Registers a new user.
Request Body:
json
{
  "username": "user1",
  "email": "user1@example.com",
  "password": "password123"
}
Response:
json
{
  "message": "User created successfully"
}

Login

Endpoint: /api/login
Method: POST
Description: Authenticates a user and returns a JWT token.
Request Body:
json
{
  "email": "user1@example.com",
  "password": "password123"
}

### Error Handling
400 Bad Request: For missing or invalid data in user input.
401 Unauthorized: For requests requiring authentication without a valid token.
404 Not Found: If a requested resource (remedy, user, etc.) is not found.

### Testing with Postman
Use POST /signup to create a user.
Use POST /login to log in and retrieve a JWT token.
Set the JWT token in Postman by adding it to the Authorization tab as a Bearer Token.
Use routes like GET /remedies or POST /favorites to test features.
Security Considerations
Password Hashing: User passwords are stored securely using hashed values.
JWT Tokens: JSON Web Tokens are used for authentication to protect user sessions.
Rate Limiting: Rate limiting is implemented on sensitive endpoints to prevent abuse.
Environment Variables: Sensitive data like secret keys and database credentials are stored in environment variables.
