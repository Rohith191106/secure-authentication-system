# secure-authentication-system
🔐 Description of the Code: Secure Authentication System using Flask, JWT, Bcrypt, and PostgreSQL

This code implements a secure user authentication system using the following stack:

Backend Framework: Flask (Python)

Security: bcrypt for password hashing, jwt for token-based authentication

Database: PostgreSQL (connected via psycopg2)

Configuration: Credentials and secrets imported from a separate config.py



---

🧱 Key Components

1. Database Connection

def get_db_connection():
    return psycopg2.connect(...)

Establishes a connection to the PostgreSQL database using credentials from config.py.


---

2. User Registration Endpoint (/register)

@app.route('/register', methods=['POST'])

Input: JSON with username and password.

Flow:

Validates input.

Hashes the password using bcrypt.

Inserts user credentials into the users table.

Handles duplicate user error (e.g., username already exists).




---

3. User Login Endpoint (/login)

@app.route('/login', methods=['POST'])

Input: JSON with username and password.

Flow:

Fetches stored hashed password from DB.

Verifies password using bcrypt.checkpw.

If valid, generates a JWT token with a 1-hour expiration time.

Returns the token in the response.




---

4. Protected Route (/protected)

@app.route('/protected', methods=['GET'])

Input: JWT token in the Authorization header (Bearer <token>).

Flow:

Extracts and verifies the token using jwt.decode.

Returns a welcome message if the token is valid.

Handles token expiration or invalid token errors.




---

🛡 Security Features

Password Hashing: bcrypt ensures stored passwords are not plain text.

Token-Based Authentication: JWTs provide stateless session handling.

Token Expiry: Tokens automatically expire after 1 hour for enhanced security.



---

📦 Required External Modules

Ensure these packages are installed:

pip install Flask bcrypt pyjwt psycopg2


---

📝 Example config.py File

SECRET_KEY = 'your-very-secret-key'
JWT_ALGORITHM = 'HS256'

DATABASE = {
    'host': 'localhost',
    'dbname': 'your_db_name',
    'user': 'your_db_user',
    'password': 'your_db_password'
}


---

✅ Outcome

This system provides:

Secure user registration and login

Encrypted password storage

Stateless session management with JWT

Access control to protected resources
