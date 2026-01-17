# Quran Memorization Center Management System

## Overview

This is a full-stack web application for managing a Quran memorization center (مركز التحفيظ). The system enables teachers and administrators to track students' Quran memorization progress, manage student records, and visualize performance statistics.

**Core Features:**
- Student management (add, edit, delete, bulk import via Excel)
- Progress tracking for memorization and review sessions
- Teacher/admin authentication with role-based access
- Student self-service portal for viewing personal progress
- Dashboard with performance analytics and charts
- Full RTL (Right-to-Left) Arabic interface

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework:** React 18 with TypeScript
- **Routing:** Wouter (lightweight client-side routing)
- **State Management:** TanStack React Query for server state
- **UI Components:** Shadcn/ui built on Radix UI primitives
- **Styling:** Tailwind CSS with custom Islamic-themed color palette (Emerald Green primary, Gold accent, Cream background)
- **Forms:** React Hook Form with Zod validation
- **Charts:** Recharts for data visualization
- **Fonts:** Cairo (UI text) and Amiri (decorative Arabic typography)

### Backend Architecture
- **Runtime:** Node.js with Express
- **Language:** TypeScript (ESM modules)
- **API Pattern:** REST endpoints defined in shared route contracts
- **Authentication:** Passport.js with local strategy, session-based auth using express-session
- **Password Hashing:** Node.js crypto scrypt

### Data Storage
- **Database:** PostgreSQL
- **ORM:** Drizzle ORM with drizzle-zod for schema validation
- **Session Store:** connect-pg-simple for PostgreSQL-backed sessions
- **Schema Location:** `shared/schema.ts` contains all table definitions

### Project Structure
```
├── client/           # React frontend
│   ├── src/
│   │   ├── components/   # Reusable UI components
│   │   ├── pages/        # Route page components
│   │   ├── hooks/        # Custom React hooks (auth, students, progress)
│   │   └── lib/          # Utilities and query client
├── server/           # Express backend
│   ├── index.ts      # Entry point
│   ├── routes.ts     # API route handlers
│   ├── storage.ts    # Database operations interface
│   ├── auth.ts       # Authentication setup
│   └── db.ts         # Database connection
├── shared/           # Shared code between client/server
│   ├── schema.ts     # Drizzle database schema
│   └── routes.ts     # API route contracts with Zod schemas
```

### Key Design Decisions

1. **Shared Route Contracts:** API endpoints are defined once in `shared/routes.ts` with Zod schemas for type safety across client and server.

2. **RTL-First Design:** The entire application is built for Arabic language with RTL text direction set at the HTML root level.

3. **Role-Based Access:** Two user roles exist - "admin" and "teacher" - with admin having additional capabilities like adding new teachers.

4. **Dual Login Systems:** Separate authentication flows for staff (username/password) and students (name + birth date).

5. **Excel Import:** Students can be bulk imported from Excel files using the xlsx library, supporting Arabic column headers.

## External Dependencies

### Database
- **PostgreSQL** - Primary database (requires DATABASE_URL environment variable)
- **Drizzle Kit** - Database migrations via `npm run db:push`

### Authentication
- **Passport.js** - Authentication middleware
- **express-session** - Session management
- **connect-pg-simple** - PostgreSQL session store

### Frontend Libraries
- **@tanstack/react-query** - Data fetching and caching
- **Radix UI** - Accessible UI primitives (dialog, dropdown, select, etc.)
- **recharts** - Chart components
- **xlsx** - Excel file parsing for bulk student import
- **date-fns** - Date formatting utilities
- **wouter** - Client-side routing

### Build Tools
- **Vite** - Frontend build and dev server
- **esbuild** - Server bundling for production
- **tsx** - TypeScript execution for development

### Environment Variables Required
- `DATABASE_URL` - PostgreSQL connection string
- `SESSION_SECRET` - Secret for session encryption (defaults to "r3pl1t" in development)