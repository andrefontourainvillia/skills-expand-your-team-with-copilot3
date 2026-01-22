# Mergington High School Activities Management System

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

A web application that allows students to view and sign up for extracurricular activities at Mergington High School. Teachers can manage student registrations through an authenticated interface.

## 📋 Overview

This is a full-stack web application built with Python (FastAPI) for the backend and vanilla JavaScript for the frontend. The system manages extracurricular activities, student registrations, and teacher authentication.

## 🛠️ Technology Stack

### Backend
- **FastAPI** - Modern, fast web framework for building APIs with Python
- **Uvicorn** - ASGI server for running FastAPI applications
- **PyMongo** - MongoDB driver for Python
- **Argon2** - Password hashing library for secure authentication

### Frontend
- **HTML5** - Structure and layout
- **CSS3** - Styling and responsive design
- **JavaScript (ES6+)** - Client-side logic and API interactions

### Database
- **MongoDB** - NoSQL database for storing activities and teacher accounts

## 📁 Project Structure

```
skills-expand-your-team-with-copilot3/
├── src/
│   ├── app.py                    # Main FastAPI application entry point
│   ├── requirements.txt          # Python dependencies
│   ├── backend/
│   │   ├── __init__.py
│   │   ├── database.py          # MongoDB configuration and data initialization
│   │   └── routers/
│   │       ├── __init__.py
│   │       ├── activities.py    # Activity management endpoints
│   │       └── auth.py          # Authentication endpoints
│   └── static/
│       ├── index.html           # Main HTML interface
│       ├── app.js               # Frontend JavaScript logic
│       └── styles.css           # Application styles
├── docs/
│   └── how-to-develop.md        # Development guide
└── README.md                    # This file
```

## 🔑 Main Files Description

### Backend Files

#### `src/app.py`
Main application entry point that:
- Initializes the FastAPI application
- Mounts static files for the frontend
- Includes API routers for activities and authentication
- Initializes the database with sample data
- Configures the root endpoint to serve the frontend

#### `src/backend/database.py`
Database configuration file that:
- Establishes MongoDB connection
- Defines database collections (activities and teachers)
- Initializes sample data for 13 different activities
- Creates default teacher accounts with hashed passwords
- Provides password hashing utilities using Argon2

#### `src/backend/routers/activities.py`
Activity management endpoints:
- `GET /activities` - Retrieve all activities with optional filters (day, start_time, end_time)
- `GET /activities/days` - Get list of days with scheduled activities
- `POST /activities/{activity_name}/signup` - Sign up a student for an activity (requires teacher auth)
- `POST /activities/{activity_name}/unregister` - Remove a student from an activity (requires teacher auth)

#### `src/backend/routers/auth.py`
Authentication endpoints:
- `POST /auth/login` - Teacher login with username and password
- `GET /auth/check-session` - Validate teacher session

### Frontend Files

#### `src/static/index.html`
Main user interface featuring:
- Header with school branding and login controls
- Sidebar with search and filter options (category, day, time)
- Main content area displaying activity cards
- Modal dialogs for registration and teacher login
- Responsive layout for mobile and desktop

#### `src/static/app.js`
Frontend JavaScript that handles:
- Loading and displaying activities from the API
- Search and filter functionality (category, day, time range)
- Student registration modal and form submission
- Teacher authentication and session management
- Dynamic activity card rendering with participant counts
- Real-time filter updates without page refresh

#### `src/static/styles.css`
Application styling including:
- Modern, clean design with card-based layout
- Responsive grid system for activities
- Modal dialog styles
- Filter button states and interactions
- Color-coded activity categories

## ✨ Features

### For Students
- 📅 Browse all available extracurricular activities
- 🔍 Search activities by name or description
- 🗂️ Filter activities by category (Sports, Arts, Academic, Community, Technology)
- 📆 Filter by day of the week
- ⏰ Filter by time (Before School, After School, Weekend)
- 👥 View current participant counts for each activity
- ✉️ Sign up for activities using school email

### For Teachers
- 🔐 Secure login system with password authentication
- ✅ Register students for activities
- ❌ Remove students from activities
- 👤 Role-based access (teacher/admin roles)

### Activity Information Displayed
- Activity name and description
- Schedule (days and time slots)
- Maximum participant capacity
- Current number of participants
- Category badge

## 🚀 Setup and Installation

### Prerequisites
- Python 3.8 or higher
- MongoDB running on localhost:27017
- pip (Python package manager)

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd skills-expand-your-team-with-copilot3
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r src/requirements.txt
   ```

3. **Start MongoDB**
   Ensure MongoDB is running on `mongodb://localhost:27017/`

4. **Run the application**
   ```bash
   python -m uvicorn src.app:app --host 0.0.0.0 --port 8000
   ```

5. **Access the application**
   - Web Interface: http://localhost:8000
   - API Documentation: http://localhost:8000/docs
   - Alternative API Docs: http://localhost:8000/redoc

## 📚 API Documentation

### Activities Endpoints

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| GET | `/activities` | Get all activities with optional filters | No |
| GET | `/activities/days` | Get list of available days | No |
| POST | `/activities/{activity_name}/signup?email=student@mergington.edu&teacher_username=mchen` | Sign up a student | Yes (teacher) |
| POST | `/activities/{activity_name}/unregister?email=student@mergington.edu&teacher_username=mchen` | Unregister a student | Yes (teacher) |

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/login` | Teacher login (pass `username` and `password` as query parameters or request body) |
| GET | `/auth/check-session` | Validate session (pass `username` as query parameter) |

**Note**: For production use, authentication credentials should be passed in the request body or via secure headers, not in URL query parameters.

### Default Teacher Accounts

| Username | Password | Role | Display Name |
|----------|----------|------|--------------|
| mrodriguez | art123 | teacher | Ms. Rodriguez |
| mchen | chess456 | teacher | Mr. Chen |
| principal | admin789 | admin | Principal Martinez |

## 🗄️ Database Schema

### Activities Collection
```javascript
{
  "_id": "Activity Name",
  "description": "Activity description",
  "schedule": "Human-readable schedule",
  "schedule_details": {
    "days": ["Monday", "Wednesday"],
    "start_time": "15:30",
    "end_time": "17:00"
  },
  "max_participants": 20,
  "participants": ["email1@mergington.edu", "email2@mergington.edu"]
}
```

### Teachers Collection
```javascript
{
  "_id": "username",
  "username": "username",
  "display_name": "Display Name",
  "password": "hashed_password",
  "role": "teacher" // or "admin"
}
```

## 🔧 Development

For detailed development instructions, see the [Development Guide](docs/how-to-develop.md).

### Quick Start Development
1. Open in GitHub Codespaces
2. Dependencies are auto-installed
3. Use VS Code's Run and Debug (F5) to start the application
4. Make changes - auto-reload is enabled

## 📝 Notes

- All data is stored in MongoDB
- The database is initialized with 13 sample activities on first run
- Student emails must use the @mergington.edu domain
- Teacher authentication is required for registration/unregistration operations
- Passwords are securely hashed using Argon2

## 🤝 Contributing

This is an educational project. Feel free to fork and experiment!

---

[![](https://img.shields.io/badge/Go%20to%20Exercise-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/andrefontourainvillia/skills-expand-your-team-with-copilot3/issues/1)

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

