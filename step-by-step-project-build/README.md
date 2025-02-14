<h1>
  <span class="headline">FastAPI Peer2Peer Payment Project</span>
  <span class="subhead">Step By Step Project Build</span>
</h1>

## Project Instructions

In this project, you will build a simple version of a peer-to-peer payment system where users can send money to each other, check their account balances, and review their most recent transactions. The application will be developed using **FastAPI** to create a **secure RESTful API**, implementing authentication and authorization to ensure that only authorized users can access certain endpoints. The project will adhere to best practices for secure API development, including the use of token-based authentication and secure database interactions.

### What You'll Learn:

By completing this project, you’ll:

- Build a **secure API** using FastAPI and implement **JWT authentication**.
- Handle **banking-like transactions**, including sending money and viewing balances.
- Write automated tests for your API endpoints using **Pytest** and **HTTPX**.

### Getting Started

This project will combine the core concepts you’ve learned in class, such as authentication, authorization, and testing, into a fully functional application. Follow the steps below to begin building and testing your Peer2Peer Payment API.

## 1. Initialize FastAPI Project

### 1.1 Set Up Your Python Environment and Install Dependencies

Create a virtual environment and install the necessary dependencies for your project:

```bash
pip install fastapi uvicorn sqlalchemy psycopg2-binary pydantic passlib bcrypt pyjwt
pip install pytest starlette httpx
```

### 1.2 Organize Your Project Structure

Organize your app into the following folder structure to keep the project modular:

```text
/project
├── config/
├── controllers/
├── data/
├── dependencies/
├── models/
├── serializers/
├── tests/
├── database.py
├── main.py
├── seed.py
├── Pipfile
```

### 1.3 Create a FastAPI App

In `main.py`, initialize the FastAPI app and include routers for handling the endpoints:

```python
from fastapi import FastAPI
from routes import users, transactions

app = FastAPI()

app.include_router(users.router, prefix="/users")
app.include_router(transactions.router, prefix="/transactions")
```

## 2. Define Your API Theme

For this project, you are building a **Peer2Peer Payment** system with the following key features:

- **User registration and login**
- **JWT-based authentication**
- **Balance check**
- **Transfer money between users**
- **View transaction history**

You will implement **basic authentication and authorization** for access control.

### Proposed API Endpoints:

Your API should support the following or similar routes for functionality:

| HTTP Method                                                | Endpoint                         | Description                                | Who Can Access? | Notes                                                                  |
| ---------------------------------------------------------- | -------------------------------- | ------------------------------------------ | --------------- | ---------------------------------------------------------------------- |
| **Auth Routes**                                            |
| `POST`                                                     | `/auth/signup`                   | Register a new user                        | Public          | Stores hashed password                                                 |
| `POST`                                                     | `/auth/login`                    | Log in and receive JWT token               | Public          | Returns access token                                                   |
| **User & Account Routes**                                  |
| `GET`                                                      | `/users/me`                      | Get current user’s profile                 | Logged-in users | Returns username, email, and account ID                                |
| `GET`                                                      | `/accounts/me`                   | View current user’s account balance        | Logged-in users | Shows balance, currency, and account details                           |
| **Transaction Routes**                                     |
| `POST`                                                     | `/transactions/send`             | Transfer money to another user             | Logged-in users | Requires sender’s ID, recipient’s ID, and amount. Prevents overdrafts. |
| `GET`                                                      | `/transactions/history`          | View transaction history (sent & received) | Logged-in users | Users can only view their own transactions                             |
| **Stretch Goals: Admin Routes & External API Integration** |
| `GET`                                                      | `/transactions/{user_id}`        | View another user’s transactions           | Admins only     | For monitoring fraud or disputes                                       |
| `GET`                                                      | `/exchange-rate?from=USD&to=EUR` | Fetch real-time exchange rate              | Logged-in users | Uses an external API to get live exchange rates (if implemented)       |

### Optional Stretch Goal: Attribute-Based Access Control (ABAC)

For an additional challenge, you can implement **Attribute-Based Access Control (ABAC)**, which allows you to restrict certain actions based on user attributes (such as `is_admin`).

For example, you could implement the following:

- Restrict viewing another user's transactions to **admins** by checking the user's `is_admin` attribute in the JWT token.

This stretch goal is optional and will not be required for the basic version of the project. If you choose to implement it, make sure to test and document it properly.

## 3. Implement Your FastAPI Application

### 3.1 Define Models and Schemas

1. **Create database models in `models/`:**

   Define models for users and transactions using **SQLAlchemy**.

2. **Create named Pydantic schemas in `serializers/`:**

   Define validation schemas for request and response data.

### 3.2 Implement the Routes

1. **Create routes in `controllers/`:**

   Implement the routes for the required functionalities (such as user registration, balance check, money transfer, and viewing transactions).

### 3.3 Start Your FastAPI Server

Use `uvicorn` to start yhe server:

```bash
pipenv run uvicorn main:app --reload
```

Test your API manually using a tool like Postman or the FastAPI interactive docs at `http://127.0.0.1:8000/docs`.

## 4. Write Tests Using Pytest and HTTPX

### 4.1 Set Up the Test Directory

Create a `tests/` directory to store your test files.

### 4.2 Write Tests for the API Endpoints

1. **Create tests for each route in `tests/`:**

   For example, write tests for:

   - `POST /auth/signup` – Test user registration.
   - `POST /auth/login` – Test user login and token generation.
   - `GET /accounts/me` – Test balance retrieval for authenticated users.
   - `POST /transactions/send` – Test money transfer functionality.

## 5. Run the Tests

Execute the tests using `pytest`:

```bash
pipenv run pytest
```

Check the test results to confirm that your API behaves as expected and returns the correct responses for all operations.
