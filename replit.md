# Merchant POS System

## Overview

A point-of-sale (POS) application for merchants to process transactions by scanning customer QR codes. The system allows merchants to manage their storefronts, add products, and record sales transactions. Built with a React frontend and Express backend using PostgreSQL for data persistence.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **Animations**: Framer Motion for page transitions and micro-interactions
- **QR Scanning**: @yudiel/react-qr-scanner for customer QR code scanning
- **Forms**: React Hook Form with Zod validation

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **API Design**: REST API with typed route contracts defined in `shared/routes.ts`
- **Validation**: Zod schemas for input validation, shared between frontend and backend

### Data Storage
- **Database**: PostgreSQL
- **Schema Location**: `shared/schema.ts` using Drizzle table definitions
- **Tables**:
  - `merchants` - Store/business information with PIN authentication
  - `products` - Items available for sale per merchant
  - `transactions` - Record of completed sales with QR code data

### Authentication
- Simple PIN-based authentication per merchant
- Session stored in browser sessionStorage
- No user accounts - merchants are identified by ID and authenticated via 4-digit PIN

### Build System
- **Development**: Vite dev server with HMR
- **Production Build**: Custom build script using esbuild for server bundling and Vite for client
- **TypeScript**: Strict mode enabled with path aliases (`@/` for client, `@shared/` for shared code)

### Project Structure
```
├── client/src/          # React frontend
│   ├── components/      # Reusable UI components
│   ├── pages/           # Route page components
│   ├── hooks/           # Custom React hooks
│   └── lib/             # Utilities and query client
├── server/              # Express backend
│   ├── routes.ts        # API route handlers
│   ├── storage.ts       # Database operations
│   └── db.ts            # Database connection
├── shared/              # Shared code between frontend/backend
│   ├── schema.ts        # Drizzle database schema
│   └── routes.ts        # API contract definitions
└── migrations/          # Drizzle database migrations
```

## External Dependencies

### Database
- **PostgreSQL**: Primary data store, connection via `DATABASE_URL` environment variable
- **Drizzle Kit**: Database migrations with `npm run db:push`

### Key NPM Packages
- **@tanstack/react-query**: Server state management
- **drizzle-orm / drizzle-zod**: Type-safe database ORM with Zod schema generation
- **@radix-ui/***: Accessible UI primitives (dialog, dropdown, toast, etc.)
- **framer-motion**: Animation library
- **@yudiel/react-qr-scanner**: QR code scanning functionality
- **date-fns**: Date formatting utilities
- **zod**: Runtime type validation

### Replit-Specific
- **@replit/vite-plugin-runtime-error-modal**: Error overlay for development
- **@replit/vite-plugin-cartographer**: Development tooling