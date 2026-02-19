# BESSID'OR - Organic Food E-commerce Platform

## Overview

BESSID'OR is a multilingual e-commerce web application for traditional, healthy, and organic food products. The platform showcases premium organic products like honey, olive oil, dates, and spices with a focus on elegant presentation and a shopping cart experience. The application supports French, English, and Arabic languages.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight client-side router)
- **State Management**: TanStack React Query for server state, React Context for local state (cart, language)
- **Styling**: Tailwind CSS with custom design tokens (warm cream/gold/brown color palette)
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Animations**: Framer Motion for page transitions and micro-interactions
- **Build Tool**: Vite with custom path aliases (@/, @shared/, @assets/)

### Backend Architecture
- **Runtime**: Node.js with Express 5
- **Language**: TypeScript with ESM modules
- **API Design**: RESTful endpoints defined in shared/routes.ts with Zod schemas for validation
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Development**: Vite dev server middleware integration for HMR

### Data Storage
- **Database**: PostgreSQL (connection via DATABASE_URL environment variable)
- **Schema**: Two main tables - products and orders (defined in shared/schema.ts)
- **Migrations**: Drizzle Kit for schema management (db:push command)

### Key Design Patterns
- **Shared Types**: Schema and route definitions shared between frontend and backend in /shared directory
- **Storage Abstraction**: DatabaseStorage class implements IStorage interface for data access
- **Type-safe API**: Zod schemas used for request/response validation on both client and server
- **Internationalization**: Custom i18n context with translations for FR/EN/AR. Product translations (name, description, benefits) stored in database columns (nameFr, nameEn, descriptionFr, descriptionEn, benefitsFr, benefitsEn) with Arabic as default fallback. Helper function `getTranslatedProduct()` in `client/src/lib/productTranslations.ts`.

### Project Structure
```
client/           # React frontend
  src/
    components/   # UI components including shadcn/ui
    pages/        # Route pages (Home, Products, About, Contact)
    hooks/        # Custom React hooks for API calls
    lib/          # Utilities, cart context, i18n, product translations
server/           # Express backend
  index.ts        # Server entry point
  routes.ts       # API route definitions
  storage.ts      # Database operations
  db.ts           # Database connection
shared/           # Shared code between frontend/backend
  schema.ts       # Drizzle schema definitions
  routes.ts       # API route contracts with Zod schemas
```

## External Dependencies

### Database
- PostgreSQL database (required, configured via DATABASE_URL)
- Drizzle ORM for database operations
- connect-pg-simple for session storage capability

### UI/Frontend Libraries
- Radix UI primitives (dialog, dropdown, select, toast, etc.)
- Framer Motion for animations
- Lucide React for icons
- React Hook Form with Zod resolver for form handling
- Embla Carousel for product carousels

### Development Tools
- Vite with React plugin
- Replit-specific plugins (runtime error overlay, cartographer, dev banner)
- esbuild for production server bundling
- TypeScript with strict mode

### Fonts
- Google Fonts: Inter (body), Playfair Display (display/headings)

### Telegram Notifications
- **Service**: Telegram Bot API (free)
- **File**: server/telegram.ts
- **Environment Variables Required**:
  - TELEGRAM_BOT_TOKEN: Bot token from @BotFather
  - TELEGRAM_CHAT_ID: Your personal/group chat ID
- **Functionality**: Sends instant notifications to Telegram when new orders are placed
- **Setup**: Create bot via @BotFather, get chat ID via @RawDataBot or web.telegram.org