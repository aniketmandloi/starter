# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Development**: `npm run dev` - Starts Next.js development server with Turbopack
- **Build**: `npm run build` - Creates production build
- **Start**: `npm start` - Starts production server
- **Lint**: `npm run lint` - Runs ESLint for code quality checks
- **Database**: `npx prisma migrate dev` - Run database migrations
- **Generate Prisma Client**: `npx prisma generate` - Generate Prisma client after schema changes

## Core Architecture

This is a Next.js 15 SaaS starter kit with the following architectural patterns:

### Tech Stack

- **Framework**: Next.js 15 with App Router (app directory)
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: Clerk (conditionally enabled via config)
- **Payments**: Stripe integration (currently disabled in config)
- **Styling**: Tailwind CSS with shadcn/ui components
- **AI Integration**: Multiple AI providers via AI SDK (Anthropic, OpenAI, Groq, DeepSeek)

### Key Directories Structure

- `app/` - Next.js App Router with nested layouts and route groups
- `components/` - Reusable UI components organized by feature
- `prisma/` - Database schema and migrations
- `utils/` - Utility functions and data operations
- `lib/` - Shared libraries and configurations

### Authentication Architecture

- Conditional auth system controlled by `config.ts`
- `AuthWrapper` component wraps the app when auth is enabled
- Protected routes defined in middleware (currently `/dashboard(.*)`)
- Clerk integration with dynamic loading to handle optional auth

### Database Schema

Key models:

- `User` - Core user data with Clerk integration
- `Subscription` - Stripe subscription management
- `SubscriptionPlan` - Available subscription plans
- `Invoice` - Payment tracking

### Route Organization

- `(pages)` route group contains main application pages
- `(auth)` nested route group for authentication pages
- API routes in `app/api/` for backend functionality
- Protected dashboard routes under `/dashboard`

### Component Architecture

- `wrapper/` components for layout and authentication
- `ui/` contains shadcn/ui base components
- `auth/` contains custom auth components
- `homepage/` contains marketing page components

### Configuration

- `config.ts` enables/disables features (auth, payments)
- Environment variables for external services
- TypeScript path aliases with `@/*` pointing to root

### AI Playground

- Chat API endpoint with multiple AI provider support
- Model registry system for provider abstraction
- DeepSeek reasoning model integration with middleware

### Payment Integration

- Stripe checkout session creation
- Webhook handling for subscription events
- Support for both subscription and one-time payments

## Important Development Notes

- Auth is conditionally loaded - the app works with or without Clerk
- Database migrations should be run after schema changes
- The project uses strict TypeScript configuration
- Tailwind includes custom animations and utility plugins
- AI SDK integration supports multiple providers through registry pattern

## Claude Code Best Practices

### Development Workflow

1. **Exploration and Planning**

   - Always read relevant files before making changes
   - Use planning mode for complex implementations
   - Verify solution reasonableness during coding
   - Create a plan before starting multi-step tasks

2. **Test-Driven Development**

   - Write tests before implementation when applicable
   - Confirm tests fail initially, then implement to pass
   - Run `npm run lint` after significant changes
   - Use database migrations for schema changes

3. **Code Quality Standards**
   - Follow existing code patterns and conventions
   - Use TypeScript strictly - no `any` types without justification
   - Maintain consistent styling with Tailwind CSS classes
   - Follow React/Next.js best practices for components

### Project-Specific Guidelines

1. **Authentication Implementation**

   - Always check `config.ts` auth status before auth-related changes
   - Use `AuthWrapper` pattern for conditional auth features
   - Test both authenticated and unauthenticated states
   - Update middleware for new protected routes

2. **Database Operations**

   - Use Prisma schema for all database changes
   - Run `npx prisma migrate dev` after schema modifications
   - Generate Prisma client with `npx prisma generate`
   - Follow existing model patterns for new entities

3. **API Development**

   - Place API routes in appropriate `app/api/` directories
   - Handle both success and error cases explicitly
   - Use proper HTTP status codes and response formats
   - Implement proper error logging for debugging

4. **Component Architecture**

   - Place reusable components in `components/ui/`
   - Use feature-specific directories for complex components
   - Follow shadcn/ui patterns for consistent styling
   - Implement proper TypeScript interfaces for props

5. **Styling Guidelines**
   - Use Tailwind CSS utility classes consistently
   - Leverage existing custom animations and utilities
   - Maintain dark mode compatibility
   - Follow responsive design patterns

### Security and Environment

1. **Environment Variables**

   - Never commit sensitive keys to repository
   - Use `.env.example` as template for required variables
   - Validate environment variables in relevant files
   - Use proper types for environment variable access

2. **Payment Integration**
   - Test Stripe integration in sandbox mode
   - Handle webhook verification properly
   - Implement proper error handling for payment failures
   - Follow PCI compliance guidelines

### Documentation and Communication

1. **Code Documentation**

   - Update this CLAUDE.md when adding new patterns
   - Comment complex business logic and integrations
   - Document any non-obvious configuration requirements
   - Maintain clear commit messages

2. **Testing and Verification**
   - Test in both development and production-like environments
   - Verify database migrations work correctly
   - Test conditional features (auth enabled/disabled)
   - Validate responsive design across screen sizes

### Repository Etiquette

1. **File Organization**

   - Follow established directory structure
   - Group related functionality together
   - Use descriptive file and folder names
   - Maintain consistent naming conventions

2. **Development Environment**
   - Use Node.js 18+ for compatibility
   - Install dependencies with `npm install`
   - Run development server with `npm run dev`
   - Use TypeScript for all new files
