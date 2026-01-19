# Quran Center Student Portal

## Overview

A student portal for a Quran memorization center (مركز القرآن الكريم) built with React and Express. The application allows students to track their Quran memorization progress, recording which surahs they've completed and when they last studied. The interface is designed for Arabic speakers with RTL layout support.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack React Query for server state and caching
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style)
- **Animations**: Framer Motion for smooth page transitions and UI animations
- **Form Handling**: React Hook Form with Zod validation
- **Typography**: Plus Jakarta Sans for body text, Amiri serif font for Arabic/Islamic headers

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **API Design**: REST API with typed route definitions in shared/routes.ts
- **Database ORM**: Drizzle ORM with PostgreSQL
- **Schema Validation**: Zod schemas shared between client and server via drizzle-zod

### Authentication
- **Provider**: Replit Auth (OpenID Connect)
- **Session Storage**: PostgreSQL-backed sessions via connect-pg-simple
- **Protected Routes**: Middleware-based authentication checks on API routes

### Data Storage
- **Database**: PostgreSQL
- **Tables**: 
  - `users` - User profiles from Replit Auth
  - `sessions` - Session storage for authentication
  - `student_progress` - Tracks surah completion status per student

### Build System
- **Development**: Vite for frontend with HMR
- **Production**: esbuild bundles server, Vite builds client
- **Output**: Single `dist` directory with bundled server and static client files

## External Dependencies

### Database
- PostgreSQL via `DATABASE_URL` environment variable
- Drizzle Kit for schema migrations (`npm run db:push`)

### Authentication
- Replit OpenID Connect provider
- Requires `REPL_ID`, `ISSUER_URL`, and `SESSION_SECRET` environment variables

### UI Components
- Radix UI primitives for accessible components
- Lucide React for icons
- date-fns for date formatting

### Key npm packages
- `drizzle-orm` / `drizzle-zod` - Database ORM and schema validation
- `express-session` / `connect-pg-simple` - Session management
- `openid-client` / `passport` - Authentication
- `@tanstack/react-query` - Data fetching and caching
- `framer-motion` - Animations
- `wouter` - Lightweight routing