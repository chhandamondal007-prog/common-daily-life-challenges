# DailyLife Solutions

A responsive Next.js starter for a daily-life challenge-solving web app. Includes a polished interactive frontend, a daily planner, searchable solution cards, saved solutions, a server-side AI endpoint, and a Supabase database schema for accounts and persistent data.

## Included now

- Responsive landing page and mobile navigation
- Searchable practical solutions and category filters
- Solution detail modal with save/bookmark interactions
- Daily task list with add, complete, delete, and progress tracking
- AI helper interface and server-side `/api/solve` route
- Graceful non-AI fallback if no AI key is configured
- Supabase SQL schema for profiles, tasks, saved solutions, and user-submitted problems
- Environment-variable template

## Requirements

- Node.js 20 or newer
- npm
- Optional: Supabase project for authentication and persistent storage
- Optional: OpenAI API key for personalized AI answers

## Run locally

1. Extract this ZIP.
2. Open a terminal in the project directory.
3. Install dependencies:

   ```bash
   npm install
   ```

4. Create a local environment file:

   ```bash
   cp .env.example .env.local
   ```

   On Windows PowerShell, use `Copy-Item .env.example .env.local`.

5. Start the development server:

   ```bash
   npm run dev
   ```

6. Open `http://localhost:3000` in your browser.

The site works as a frontend demo without Supabase or an AI key. Tasks and bookmarks currently live in component state, so they reset when the page reloads.

## Enable the AI helper

Add your key to `.env.local`:

```env
OPENAI_API_KEY=your_secret_key
OPENAI_MODEL=gpt-4o-mini
```

Restart `npm run dev`. Keep the key server-side: never use a `NEXT_PUBLIC_` prefix for secrets. AI provider usage may incur charges. The endpoint limits prompt size and handles provider errors, but production deployments should also add authentication, rate limiting, abuse monitoring, and a clear privacy notice.

## Set up Supabase

1. Create a project in Supabase.
2. Open the SQL Editor and run `supabase/schema.sql`.
3. Add the project URL and public anon key to `.env.local`.
4. Implement Supabase SSR auth and replace the current in-memory task/bookmark state with authenticated database queries before treating accounts as production-ready.

Environment variables:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-public-anon-key
```

The database schema enables Row Level Security for user-owned records. Admin role assignment and moderation authorization are intentionally not exposed in this starter; implement them on the server before enabling an admin dashboard.

## Production checklist

- Implement sign-up, sign-in, sign-out, password recovery, and profile management.
- Persist planner tasks and saved solutions in Supabase.
- Add server-side role checks for admin routes and moderation actions.
- Add request rate limits, abuse protection, monitoring, and backups.
- Add privacy policy, terms, consent/retention rules, and account deletion.
- Validate accessibility, mobile layouts, and error states.
- Run `npm run build` and test the deployed environment.
- Never commit `.env.local`, provider API keys, or a database service-role key.

## Project structure

```text
app/
  api/solve/route.ts   # Server-side AI endpoint
  globals.css          # Responsive styling
  layout.tsx            # Metadata and global layout
  page.tsx              # Main interactive experience
lib/                    # Reserved for shared helpers and Supabase clients
supabase/schema.sql     # Database tables and Row Level Security
.env.example            # Environment variable template
```

## Important

This is a starter project, not a fully deployed production service. The landing experience and local interactions are implemented; real authentication, cross-device persistence, and a secure admin workflow require the setup and integration steps above. General wellness or productivity suggestions are not a substitute for qualified professional help.
