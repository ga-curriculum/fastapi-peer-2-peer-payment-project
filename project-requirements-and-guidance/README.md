<h1>
  <span class="headline">FastAPI Peer2Peer Payment Project</span>
  <span class="subhead">Project Requirements and Guidance</span>
</h1>

## Overview

### Objective:

In this project, you will build and test a **secure** RESTful API using **FastAPI**. You will implement **authentication and authorization**, ensuring that only authorized users can access certain endpoints. Your application will follow best practices for **secure API development**, including token-based authentication, role-based access control, and secure database interactions.

### Scope and Complexity:

For your project, you will be building a FastAPI-based web service using **Python**, **FastAPI**, **JWT-based authentication**, and **SQLAlchemy** for database management.

Throughout the course, you've learned how to build and test APIs. Now, it's your turn to **apply that knowledge** by developing an API with robust security features.

The project is estimated to take around **10-15 hours** to complete.

**_You will work individually on this project._**

> ❗ **General Assembly has a zero-plagiarism policy.**  
> Your project must be **your own** work. While it’s fine to use libraries or small code snippets to accomplish specific tasks, your project’s core functionality should be implemented by you.

A printable version of the project requirements can be found [here](./assets/project-requirements.pdf).

## Technical Requirements

> ✅ More than **three** incomplete items in this section will result in a failing grade.

Your application must meet the following requirements:

- The project must be committed to a version control system (**Git**) with clear commit messages reflecting progress.
- The project must follow a **modular structure**, with separate folders for controllers, models, and tests.
- The project must include **JWT-based authentication** for user login and attribute-based access control.
- Authenticated users must be able to perform the following minimum actions: **transfer money to another user**, **view their account balance**, and access a **list of all transactions** associated with their account
- The project must include **unit tests** for all API endpoints using **PyTest**.
- Tests should cover common **success cases** as well as **error cases**.

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

#### Stretch Goals:

- `GET /exchange-rate?from=USD&to=EUR` – Fetch real-time exchange rate using an external API (if implemented).

- `GET /transactions/{user_id}` - Retrieve all transactions associated with a specific user. This endpoint is restricted to Admin users only.
- To determine which users are admins, you can implement attribute-based access control (ABAC). If you're using ABAC, you would assign a boolean attribute (like is_admin) to specific users.
- When a user logs in, you generate a JWT token containing their user_id and is_admin status. This will be included in the token payload.

## Code Convention and API Design Requirements

> ✅ More than **two** incomplete items in this section will result in a failing grade.

- The code must be **well-organized and modular**, following FastAPI best practices.
- Functions and routes should be clearly separated into different **files (ex: controllers, models, tests)**.
- **Error messages should be clear and informative**, guiding users to correct their input.
- Sensitive data (ex: passwords) must be **securely stored using hashing (ex: bcrypt)**.
- Database interactions should be **safe**, preventing SQL injection and other vulnerabilities.

## README Requirements

> ✅ More than **three** incomplete items in this section will result in a failing grade.

Your project must include a `README.md` file with:

- The **app’s name**.
- A brief **description** of your app and its functionality.
- A **Getting Started** section with instructions on how to install dependencies and run the app locally.
- A **Technologies Used** section listing major frameworks and libraries, such as FastAPI, SQLAlchemy, and PyTest.
- If applicable, an **Attributions** section crediting external resources or libraries that require acknowledgment.

## Evaluation

Your instructional team will evaluate your project after the due date. They will use the above guidelines to determine whether your project meets the **minimum requirements**.

If there is a specific section of code where you’d like additional feedback, **ask your instructor for a code review**!

## Guidance

### Getting Started

Here are some quick tips to help you plan and execute your project successfully:

- **Discuss your app idea with an instructor** before diving too deep into development.
- **_Keep it simple._** A well-functioning **Minimum Viable Product (MVP)** is better than an unfinished app with unnecessary features.
- **Prioritize core functionality** first. Develop features in a way that allows you to test as you go.
- **Regularly review the project requirements** to stay on track. A printable version of this document is available [here](./assets/project-requirements.pdf).
- **Use clear commit messages** to track your progress.

### Project Assistance

Your instructor team will provide **guidelines for reaching out for help** during the project. Make sure to:

- **Ask specific questions** when seeking assistance.
- **Follow debugging best practices** before reaching out—check error messages and logs!
