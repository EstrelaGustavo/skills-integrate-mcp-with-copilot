# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teacher-only sign-up and removal of participants

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure teacher credentials in the environment. Do not commit these values:

   ```sh
   export TEACHER_USERNAME="teacher"
   export TEACHER_PASSWORD="choose-a-strong-password"
   ```

3. Run the application from the repository root:

   ```
   uvicorn app:app --app-dir src --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth`                                                           | Validate teacher credentials                                       |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (teacher credentials required)                    |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Remove a student (teacher credentials required)                  |

The activity list remains public. Sign-up and removal require HTTP Basic
credentials configured through `TEACHER_USERNAME` and `TEACHER_PASSWORD`.
Use HTTPS when exposing the application outside a trusted local environment.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
