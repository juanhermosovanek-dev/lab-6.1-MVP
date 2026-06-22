# EduPath Argentina

Student progress and reporting platform for Argentine private secondary schools. 
This application helps Academic Directors generate comprehensive student progress reports by consolidating data from attendance, grading, and teacher observations in under 90 seconds.

## Features

- **Authentication**: Secure sign up, log in, and log out using Supabase Auth. Data is strictly isolated per school/user.
- **Database**: Persistent storage of `students` and their `observations` using Supabase PostgreSQL, protected via Row Level Security (RLS).
- **Transaction Flow**: Complete CRUD operations functionality through the UI — Add students, log teacher observations, and delete records safely.
- **Basic Analytics**: PostHog integration capturing key user interactions (`user_signed_up`, `user_logged_in`, `student_added`, `student_selected`, `observation_submitted`, `report_generated`, `user_logged_out`).
- **Automated Reporting**: Instant report generation aggregating student's academic standing, grade drops, attendance rates, and qualitative teacher observations.

## Tech Stack

- **Framework**: React 19 + Vite + TypeScript
- **Styling**: Tailwind CSS v4
- **Database & Auth**: Supabase (PostgreSQL)
- **Analytics**: PostHog

## Local Development Setup

To run this application locally, follow these steps:

### 1. Clone the repository

```bash
git clone <repository_url>
cd edupath-argentina
```

### 2. Install dependencies

```bash
npm install
```

### 3. Environment Variables

Create a `.env` or `.env.local` file in the root of the project and add your credentials:

```bash
# Supabase Configuration
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key

# PostHog Configuration
VITE_POSTHOG_KEY=your_posthog_project_api_key
VITE_POSTHOG_HOST=https://us.i.posthog.com
```

**Database Schema Setup (Supabase):**
Ensure your Supabase project has the following tables created:
1. `students` (id, user_id, name, year, subject, attendance, grade_t1, grade_t2, status, created_at)
2. `observations` (id, student_id, teacher_name, content, created_at)

Enable **Row Level Security (RLS)** on both tables, ensuring users can only manage their own students and associated observations.

### 4. Start the development server

```bash
npm run dev
```

The application will be available at `http://localhost:3000`.

## Architecture & Compliance

- **Data Segregation:** The application strictly enforces isolation of school records using Supabase Auth and Row Level Security tied to the authenticated user ID.
- **Ley 25,326 Compliance:** The application and its generated reports display notifications regarding the Argentine personal data privacy law (Ley 25,326), confirming compliance principles. No data represents third-party ownership.
