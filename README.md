# Mandarin Academy
andarin Academy Frontend is a responsive, modern web application built with **Next.js** and **Tailwind CSS**. It serves as the user-facing platform for the Mandarin Academy ecosystem, providing intuitive interfaces for both students tracking their language learning journey and administrators managing platform resources.
Mandarin academy's web Backend is using a REST API service built with NestJS and Prisma to support a modern online Mandarin learning platform. The backend handles authentication, course management, lesson organization, user progress tracking, and admin management.

---
## ✨ Features

For Students
* Course Discovery: Browse and search through available courses
* Video Learning: Watch video lessons with progress tracking
* Progress Tracking: Monitor your learning progress across courses
* Dashboard: Personal dashboard showing enrolled courses and statistics
* User Profile: Manage your personal information and learning history

For Administrators
* User Management: Create, update, and delete user accounts
* Course Management: Full CRUD operations for courses
* Lesson Management: Complete lesson lifecycle management
* Analytics Dashboard: View system-wide statistics and metrics
* Role-based Access: Control access based on user roles (student, instructor, admin)

## ✨ Technical Features

* Authentication: JWT-based authentication with NextAuth.js
* Video Progress: Track watch time and completion status
* Responsive Design: Mobile-friendly interface with Tailwind CSS
* Real-time Updates: Dynamic content updates and progress tracking
* API Documentation: Swagger/OpenAPI documentation for the REST API
* Database Migrations: Prisma-based database management

## 🎨 UI Components

The frontend uses a comprehensive design system built with:
- **Radix UI**: Accessible, unstyled UI primitives
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide Icons**: Beautiful, customizable icons
- **Responsive Design**: Mobile-first approach

## 📱 Pages Overview

### Public Pages
- **Home**: Landing page with featured courses
- **Courses**: Browse all available courses
- **Auth**: Sign in and sign up pages

### Protected Pages
- **Dashboard**: Personal learning dashboard
- **Profile**: User profile management
- **Course Detail**: Individual course page with lessons
- **Video Player**: Video lesson player with progress tracking

### Admin Pages
- **Admin Dashboard**: System overview and statistics
- **User Management**: CRUD operations for users
- **Course Management**: CRUD operations for courses
- **Lesson Management**: CRUD operations for lessons

---
```text
## 📁 Frontend and Backend Structure

Mandarin-Academy/
├── backend/                # NestJS backend application
│   ├── src/
│   │   ├── admin/          # Admin management module
│   │   ├── auth/           # Authentication module
│   │   ├── courses/        # Course management module
│   │   ├── enrollments/    # Enrollment management module
│   │   ├── lessons/        # Lesson management module
│   │   ├── progress/       # Progress tracking module
│   │   ├── users/          # User management module
│   │   └── prisma/         # Prisma service
│   ├── prisma/             # Database schema and migrations
│   └── package.json
├── frontend/               # Next.js frontend application
│   ├── app/                # App router pages
│   │   ├── admin/          # Admin panel pages
│   │   ├── auth/           # Authentication pages
│   │   ├── courses/        # Course pages
│   │   ├── dashboard/      # User dashboard
│   │   └── profile/        # User profile
│   ├── components/         # Reusable UI components
│   │   ├── admin/          # Admin-specific components
│   │   ├── auth/           # Authentication components
│   │   ├── courses/        # Course-related components
│   │   ├── home/           # Homepage components
│   │   ├── layout/         # Layout components
│   │   └── ui/             # Base UI components
│   ├── lib/                # Utility functions and API client
│   └── package.json
└── README.md
```
---
## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```
##  Deployement
- Backend deployment: https://crack-be-clarissawi609-source-production.up.railway.app/
  ![image alt](https://github.com/Revou-FSSE-Oct25/crack-fe-clarissawi609-source/blob/main/Images/Screenshot%202026-05-19%20203047.png?raw=true)
- Frontend deployment: https://crack-fe-clarissawi609-source-10ki7115i.vercel.app
  ![image alt](https://github.com/Revou-FSSE-Oct25/crack-fe-clarissawi609-source/blob/main/Images/Screenshot%202026-05-23%20225301.png?raw=true)
- swagger api: https://crack-fe-clarissawi609-source-10ki7115i.vercel.app
-   ![image alt](https://github.com/Revou-FSSE-Oct25/crack-fe-clarissawi609-source/blob/main/Images/Screenshot%202026-05-23%20234239.png?raw=true)


## 📊 Database Schema

The application uses the following main entities:

- **User**: Stores user information and authentication data
- **Course**: Contains course information and metadata
- **Lesson**: Individual lessons within courses
- **Enrollment**: Links users to courses they're enrolled in
- **VideoProgress**: Tracks video watch progress for each user and lesson

## 🔐 Authentication & Authorization

- **JWT Authentication**: Secure token-based authentication
- **Role-based Access**: Three user roles supported:
  - `student`: Default role for learners
  - `instructor`: Can create and manage courses
  - `admin`: Full system access
- **Protected Routes**: API endpoints and frontend pages are protected based on user roles

## 🎯 API Endpoints

### Authentication
- `POST /auth/register` - User registration
- `POST /auth/login` - User login

### Courses
- `GET /courses` - Get all courses
- `GET /courses/:id` - Get course by ID
- `POST /courses` - Create new course (auth required)
- `PUT /courses/:id` - Update course (auth required)
- `DELETE /courses/:id` - Delete course (auth required)

### Lessons
- `GET /lessons` - Get lessons (filtered by course)
- `POST /lessons` - Create new lesson (auth required)
- `PUT /lessons/:id` - Update lesson (auth required)
- `DELETE /lessons/:id` - Delete lesson (auth required)

### Enrollments
- `POST /enrollments` - Enroll in course (auth required)
- `GET /enrollments/my-courses` - Get user's enrolled courses (auth required)
- `PUT /enrollments/progress` - Update course progress (auth required)

### Admin
- `GET /admin/dashboard` - Get admin dashboard stats (admin only)
- `GET /admin/users` - Get all users (admin only)
- `POST /admin/users` - Create user (admin only)
- `GET /admin/courses` - Get all courses (admin only)
- `GET /admin/lessons` - Get all lessons (admin only)

---
### Entity Relationship Diagram (ERD)

```mermaid
erDiagram
    USER {
        int id PK
        string name
        string email
        string password
        enum role
        datetime createdAt
        datetime updatedAt
    }

    COURSE {
        int id PK
        string title
        string description
        string thumbnail
        int instructorId FK
        datetime createdAt
        datetime updatedAt
    }

    LESSON {
        int id PK
        string title
        string videoUrl
        int duration
        int courseId FK
        int order
        datetime createdAt
    }

    ENROLLMENT {
        int id PK
        int userId FK
        int courseId FK
        float progressPercentage
        datetime enrolledAt
        datetime completedAt
    }

    VIDEO_PROGRESS {
        int id PK
        int userId FK
        int lessonId FK
        int watchedSeconds
        boolean completed
        datetime updatedAt
    }

    USER ||--o{ ENROLLMENT : "enrolls"
    COURSE ||--o{ ENROLLMENT : "has"

    COURSE ||--o{ LESSON : "contains"

    USER ||--o{ VIDEO_PROGRESS : "tracks"
    LESSON ||--o{ VIDEO_PROGRESS : "has"
    
    USER ||--o{ COURSE : "teaches"
````
---
### User Flow

```mermaid
graph TD
    %% Public Access
    Start([Public Landing Page]) --> Browse[Browse Courses Public]
    Browse -->|Clicks Enroll or Sign In| Auth[Auth Page: Sign In / Sign Up]
    
    %% Authentication Split
    Auth -->|Authentication Success| RoleCheck{What is the<br/>user role?}
    
    %% Student Path
    RoleCheck -->|student| StudentDash[Student Dashboard]
    StudentDash --> Profile[Profile Settings & History]
    StudentDash --> CourseDetail[Course Details Page]
    CourseDetail -->|Clicks Watch| VideoPlayer[Video Player]
    VideoPlayer -->|API Call| Progress[Updates Video Progress]

    %% Admin / Instructor Path
    RoleCheck -->|admin / instructor| AdminDash[Admin Dashboard]
    AdminDash --> UserMgmt[User Management CRUD]
    AdminDash --> CourseMgmt[Course Management CRUD]
    AdminDash --> LessonMgmt[Lesson Management CRUD]

    %% Styling for better visibility
    style RoleCheck fill:#f9f,stroke:#333,stroke-width:2px
    style Start fill:#bbf,stroke:#333,stroke-width:2px
    style Progress fill:#bfb,stroke:#333,stroke-width:2px
````

---

## 🎯 Project Purpose

This backend was customized and developed as part of a modern Mandarin learning platform project using NestJS and Prisma.

---

## 👩‍💻 Developer

Backend developed for educational and learning purposes.
