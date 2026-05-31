# Seerah Companion — Setup Guide

## Stack
- **Next.js 14** — React framework
- **NextAuth.js** — Google OAuth + Email/Password auth
- **Prisma** — ORM / database client
- **PostgreSQL** on **Supabase** (free tier)
- **Deployed on Vercel** (free tier)

---

## Step 1 — Get a Free Database (Supabase)

1. Go to [supabase.com](https://supabase.com) → New project
2. Create a project, choose a region close to you
3. Go to **Settings → Database → Connection string → URI**
4. Copy the connection string — looks like:
   `postgresql://postgres:[PASSWORD]@db.[PROJECT].supabase.co:5432/postgres`

---

## Step 2 — Google OAuth Credentials

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project → APIs & Services → Credentials
3. Create OAuth 2.0 Client ID → Web Application
4. Authorized redirect URIs:
   - `http://localhost:3000/api/auth/callback/google` (dev)
   - `https://your-app.vercel.app/api/auth/callback/google` (production)
5. Copy Client ID and Client Secret

---

## Step 3 — Anthropic API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. API Keys → Create Key
3. Copy the key

---

## Step 4 — Local Setup

```bash
# Install dependencies
npm install

# Copy env file
cp .env.example .env.local

# Fill in .env.local:
DATABASE_URL="postgresql://..."
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="run: openssl rand -base64 32"
GOOGLE_CLIENT_ID="..."
GOOGLE_CLIENT_SECRET="..."
ANTHROPIC_API_KEY="sk-ant-..."

# Push database schema
npx prisma db push

# Run development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## Step 5 — Deploy to Vercel

1. Push this folder to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → Import Project → select your repo
3. Add all environment variables from `.env.local` in Vercel dashboard
4. Change `NEXTAUTH_URL` to your Vercel URL (e.g. `https://seerah-companion.vercel.app`)
5. Add your Vercel URL to Google OAuth authorized redirect URIs
6. Deploy!

---

## Project Structure

```
src/
├── app/
│   ├── (auth)/
│   │   ├── login/page.tsx       # Sign in page
│   │   └── register/page.tsx    # Create account page
│   ├── api/
│   │   ├── auth/
│   │   │   ├── [...nextauth]/   # NextAuth handler
│   │   │   └── register/        # Email registration
│   │   └── chats/
│   │       ├── route.ts         # GET all chats, POST new chat
│   │       └── [chatId]/
│   │           ├── route.ts     # PATCH rename, DELETE chat
│   │           └── messages/    # GET messages, POST & get AI reply
│   ├── chat/page.tsx            # Main chat UI
│   └── page.tsx                 # Redirects to /chat or /login
├── components/
│   └── Providers.tsx            # SessionProvider wrapper
└── lib/
    ├── auth.ts                  # NextAuth config
    ├── prisma.ts                # Prisma client singleton
    └── seerah-prompt.ts         # AI system prompt (Sirat un Nabi)

prisma/
└── schema.prisma                # Database schema (User, Chat, Message)
```

---

## Features
- Google OAuth sign in
- Email + password sign in / registration
- Persistent chat history per user (stored in PostgreSQL)
- Multiple named chat sessions
- Rename & delete conversations
- AI powered by Claude Sonnet, with Sirat un Nabi system prompt
- Fully responsive — works on mobile & desktop
