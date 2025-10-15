# Repository Overview: Mergington High School Activities Management System

## Main Functionality

This repository contains a **High School Activity Management System** - a full-stack web application that enables students at Mergington High School to view and sign up for extracurricular activities. The system is built as a learning exercise for GitHub Copilot, demonstrating how AI-assisted coding can help build complete web applications.

## Key Components

### 1. Backend API (`src/app.py`)

The backend is built with **FastAPI**, a modern Python web framework, and provides a RESTful API for managing extracurricular activities.

**Core Features:**
- **In-Memory Database**: Stores activity data including name, description, schedule, max participants, and current participant list
- **Three Main Endpoints**:
  - `GET /` - Redirects to the main HTML interface
  - `GET /activities` - Returns all available activities with their details
  - `POST /activities/{activity_name}/signup` - Allows students to sign up for activities

**Activities Included:**
- **Academic**: Chess Club, Programming Class, Math Olympiad, Debate Team
- **Sports**: Gym Class, Basketball Team, Swimming Club
- **Arts**: Drama Club, Art Studio

**Data Structure:**
```python
{
    "Activity Name": {
        "description": "Activity details",
        "schedule": "When it meets",
        "max_participants": 15,
        "participants": ["student@mergington.edu"]
    }
}
```

**Validation Features:**
- Checks if activity exists before signup
- Prevents duplicate signups (same student can't sign up twice)
- Returns appropriate HTTP error codes (404 for not found, 400 for bad requests)

### 2. Frontend Web Application (`src/static/`)

A responsive single-page application (SPA) built with vanilla JavaScript, HTML, and CSS.

#### HTML Structure (`index.html`)
- **Header**: School branding and title
- **Activities Display Section**: Shows all available activities with details
- **Signup Form Section**: Allows students to register for activities
- **Footer**: Copyright information

#### JavaScript Functionality (`app.js`)
- **Dynamic Activity Loading**: Fetches activities from API on page load
- **Activity Display**: 
  - Creates cards for each activity showing description, schedule, and availability
  - Displays current participants for each activity
  - Shows remaining spots available
- **Form Handling**:
  - Validates user input
  - Submits signup requests to the backend
  - Displays success/error messages
  - Auto-hides messages after 5 seconds
- **Security**: Sanitizes HTML in participant emails to prevent XSS attacks

#### CSS Styling (`styles.css`)
- **Modern Design**: Clean, professional appearance with blue color scheme
- **Responsive Layout**: Adapts to different screen sizes
- **Card-Based UI**: Each activity displayed in an attractive card format
- **Participant Lists**: Styled lists with alternating backgrounds for readability
- **Form Elements**: Styled input fields, buttons, and feedback messages
- **Visual Feedback**: Success messages in green, errors in red

### 3. Documentation

#### `src/README.md`
Technical documentation for developers including:
- Installation instructions
- How to run the application
- API endpoint specifications
- Data model description

#### Main `README.md`
Congratulatory page indicating successful completion of the GitHub Skills exercise.

## System Architecture

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                         Browser                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  HTML (index.html)                                  │   │
│  │  - Header with school branding                      │   │
│  │  - Activities display section                       │   │
│  │  - Signup form section                              │   │
│  └──────────────────┬──────────────────────────────────┘   │
│                     │                                       │
│  ┌──────────────────▼──────────────────────────────────┐   │
│  │  JavaScript (app.js)                                │   │
│  │  - Fetch activities from API                        │   │
│  │  - Render activity cards dynamically                │   │
│  │  - Handle form submissions                          │   │
│  │  - Display success/error messages                   │   │
│  └──────────────────┬──────────────────────────────────┘   │
│                     │                                       │
│  ┌──────────────────▼──────────────────────────────────┐   │
│  │  CSS (styles.css)                                   │   │
│  │  - Responsive layout                                │   │
│  │  - Card-based activity display                      │   │
│  │  - Form styling                                     │   │
│  └─────────────────────────────────────────────────────┘   │
└──────────────────────┬──────────────────────────────────────┘
                       │ HTTP Requests
                       │ (REST API calls)
┌──────────────────────▼──────────────────────────────────────┐
│                   FastAPI Server                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  API Endpoints (app.py)                             │   │
│  │  ┌───────────────────────────────────────────────┐  │   │
│  │  │ GET /                                         │  │   │
│  │  │  └─> Redirect to /static/index.html          │  │   │
│  │  ├───────────────────────────────────────────────┤  │   │
│  │  │ GET /activities                               │  │   │
│  │  │  └─> Return all activities (JSON)            │  │   │
│  │  ├───────────────────────────────────────────────┤  │   │
│  │  │ POST /activities/{name}/signup                │  │   │
│  │  │  └─> Validate & add student to activity      │  │   │
│  │  └───────────────────────────────────────────────┘  │   │
│  └─────────────────────┬───────────────────────────────┘   │
│                        │                                    │
│  ┌─────────────────────▼───────────────────────────────┐   │
│  │  In-Memory Database                                 │   │
│  │  {                                                  │   │
│  │    "Chess Club": {...},                            │   │
│  │    "Programming Class": {...},                     │   │
│  │    "Basketball Team": {...},                       │   │
│  │    ...9 activities total                           │   │
│  │  }                                                  │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Request Flow

1. **User Opens Application**:
   ```
   Browser → GET / → FastAPI → Redirects to /static/index.html
   ```

2. **Loading Activities**:
   ```
   Browser → GET /activities → FastAPI → Returns JSON with all activities
   → JavaScript renders activity cards
   ```

3. **Student Signup**:
   ```
   User fills form → JavaScript validates → POST /activities/{name}/signup
   → FastAPI validates → Adds student to participants list
   → Returns success/error → JavaScript displays message
   ```

### Technology Stack

- **Backend**: Python 3 with FastAPI framework
- **Server**: Uvicorn ASGI server
- **Frontend**: Vanilla JavaScript (ES6+), HTML5, CSS3
- **Data Storage**: In-memory (data resets on server restart)
- **API Style**: REST with JSON

## Development Environment

The repository includes:
- **VS Code Configuration** (`.vscode/launch.json`): Debug configurations
- **Dev Container** (`.devcontainer/devcontainer.json`): Containerized development environment
- **Dependencies** (`requirements.txt`): Python package specifications

## Educational Purpose

This repository serves as a **GitHub Copilot learning exercise**, demonstrating:
- How to build a full-stack web application with AI assistance
- FastAPI backend development
- Frontend JavaScript development
- RESTful API design
- Form handling and validation
- Responsive web design

## Limitations

- **No Persistence**: Data is stored in memory and lost on restart
- **No Authentication**: Anyone can sign up with any email
- **No Capacity Enforcement**: System doesn't prevent signups when activities are full
- **Single Server**: No database, no scalability considerations

## Running the Application

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Navigate to the src directory:
   ```bash
   cd src
   ```

3. Run the server:
   ```bash
   uvicorn app:app --reload
   ```

4. Open browser to:
   - Main interface: http://localhost:8000
   - API documentation: http://localhost:8000/docs
   - Alternative docs: http://localhost:8000/redoc

## Future Enhancement Opportunities

This simple application could be extended with:
- Database integration (PostgreSQL, MongoDB)
- User authentication and authorization
- Activity capacity enforcement
- Email notifications
- Admin panel for managing activities
- Student profiles and activity history
- Waitlist functionality
- Calendar integration
- Mobile app version
