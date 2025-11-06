# BonelzBot Premium Selling Website

## Overview

This is a marketing website for BonelzBot, a premium Clash of Clans automation bot. The site is designed as a single-page application featuring a modern gaming aesthetic with conversion-focused sections including hero banner, features showcase, pricing, FAQ, and Discord community integration. The project uses a full-stack TypeScript architecture with React frontend and Express backend, currently configured as a static landing page with minimal server-side logic.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build System**
- React 18 with TypeScript for type-safe component development
- Vite as the build tool and development server, providing fast HMR and optimized production builds
- Wouter for client-side routing (lightweight alternative to React Router)
- React Query (@tanstack/react-query) for server state management and data fetching

**UI Component System**
- Shadcn/ui component library (New York style variant) for consistent, accessible UI components
- Radix UI primitives as the foundation for interactive components (dialogs, dropdowns, accordions, etc.)
- Tailwind CSS for utility-first styling with custom design tokens
- Custom color system using CSS variables supporting light/dark modes with HSL color space
- Typography system using Inter for body text and Space Grotesk/Orbitron for display headlines

**Styling Strategy**
- Tailwind CSS configured with custom spacing scale (4, 6, 8, 12, 16, 20, 24 units)
- Custom elevation system using `hover-elevate` and `active-elevate-2` classes for interactive feedback
- Responsive grid layouts: mobile-first approach with md/lg breakpoints
- Design guidelines emphasize premium gaming aesthetic with depth, dimension, and trust-building visuals

**State Management**
- React Query for async state and API communication
- React hooks (useState, useEffect) for local component state
- Custom hooks like `use-mobile` for responsive behavior detection
- Toast notifications via custom hook system (`use-toast`)

### Backend Architecture

**Server Framework**
- Express.js server with TypeScript for type safety
- ESBuild for bundling server code in production
- Custom Vite middleware integration in development for SSR-ready setup

**Development vs Production**
- Development: Vite dev server with HMR, middleware mode for seamless frontend/backend integration
- Production: Static file serving from dist/public directory after Vite build
- Replit-specific plugins for runtime error overlays, cartographer, and dev banner in development

**Request/Response Pipeline**
- JSON body parsing with raw body preservation for webhook verification
- Request logging middleware capturing method, path, status, duration, and response payload
- CORS and security headers (implicit through Express defaults)
- Session support scaffolded via connect-pg-simple (though not actively used in current implementation)

**Storage Interface**
- Abstract IStorage interface defining CRUD operations for users
- In-memory implementation (MemStorage) as default storage backend
- Database schema defined with Drizzle ORM for PostgreSQL migration path
- User model with id, username, password fields in shared schema

### Data Layer

**Database Strategy**
- Drizzle ORM for type-safe database operations and schema management
- PostgreSQL as target database (via @neondatabase/serverless for serverless deployment)
- Schema-first approach with Drizzle Kit for migrations (output to ./migrations directory)
- Zod integration via drizzle-zod for runtime validation of insert operations

**Current State**
- Storage layer implemented as in-memory Map-based system (MemStorage class)
- PostgreSQL schema defined but not actively connected
- Database provisioning expected via DATABASE_URL environment variable
- Migration system configured but not yet executed

**Data Models**
- Users table: varchar id (UUID), text username (unique), text password
- Insert schemas derived from Drizzle tables using createInsertSchema
- Type inference for User (select) and InsertUser types exported from shared schema

### External Dependencies

**Third-Party Services**
- Discord community integration: Primary conversion point directing users to discord.gg/FE7Ctv7dsE
- No payment processing integrated (purchases handled through Discord)
- No analytics or tracking services explicitly configured
- No email service integration

**UI Component Libraries**
- Radix UI: Comprehensive set of unstyled, accessible component primitives (@radix-ui/react-*)
- Lucide React: Icon library for UI elements
- React Icons: Additional icons (specifically SiDiscord for Discord branding)
- Embla Carousel: Carousel/slider functionality
- CMDK: Command menu component

**Font & Asset Management**
- Google Fonts: Inter, Space Grotesk, Orbitron, Architects Daughter, DM Sans, Fira Code, Geist Mono
- Local assets stored in attached_assets directory (bot screenshots, generated orb images)
- Vite alias configuration for @assets path resolution

**Build & Development Tools**
- TypeScript for type safety across frontend and backend
- PostCSS with Tailwind CSS and Autoprefixer
- ESBuild for server bundling in production
- Replit-specific development tooling (error modal, cartographer, dev banner)

**Database & ORM**
- Drizzle ORM: Type-safe ORM with PostgreSQL dialect
- Drizzle Kit: Migration management and schema introspection
- Neon Serverless: PostgreSQL driver for serverless environments
- Connect-pg-simple: PostgreSQL session store for Express sessions

**Validation & Forms**
- Zod: Schema validation library
- React Hook Form: Form state management
- @hookform/resolvers: Integration between React Hook Form and Zod

**Routing & Navigation**
- Wouter: Minimalist client-side routing (~1.2KB)
- Smooth scroll behavior for anchor-based navigation to page sections