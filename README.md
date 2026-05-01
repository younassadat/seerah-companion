# Seerah Companion

> An Islamic AI companion grounded in the Sirat un Nabi — the seven-volume biography of Prophet Muhammad ﷺ by Allama Shibli Nomani and Syed Sulaiman Nadvi.

![Version](https://img.shields.io/badge/version-0.1.0-6929C4?style=flat-square)
![Next.js](https://img.shields.io/badge/Next.js-14-000000?style=flat-square&logo=next.js)
![Status](https://img.shields.io/badge/status-active-1D9E75?style=flat-square)

---

## What It Is

Seerah Companion is a scholarly AI chat application built strictly on authentic Islamic sources. It is not a general-purpose chatbot — every response is grounded in the Sirat un Nabi, cross-referenced with classical hadith collections and primary Islamic biographies.

The goal is to make serious Seerah scholarship accessible — answering questions about the life of the Prophet ﷺ with depth, context, and academic rigour.

---

## Knowledge Base

The AI is grounded in the complete **Sirat un Nabi** (7 volumes):

| Volume | Author | Year | Coverage |
|---|---|---|---|
| Vol. 1 | Allama Shibli Nomani | 1918 | Pre-Islamic Arabia, early revelation, Makkan period |
| Vol. 2 | Shibli Nomani / Syed Sulaiman Nadvi | 1920 | Final years, governance in Madinah, Farewell Pilgrimage |
| Vol. 3 | Syed Sulaiman Nadvi | 1924 | Miracles and evidences of prophethood |
| Vol. 4 | Syed Sulaiman Nadvi | 1932 | Nature of prophethood, revelation, Islamic beliefs |
| Vol. 5 | Syed Sulaiman Nadvi | 1935 | Islamic worship — prayer, fasting, zakat, hajj |
| Vol. 6 | Syed Sulaiman Nadvi | 1938 | Islamic ethics and the Prophet's ﷺ character |
| Vol. 7 | Syed Sulaiman Nadvi | 1955 | Islamic law and governance (unfinished) |

Additional references: Ibn Hisham · al-Waqidi · Ibn Sa'd · Sahih al-Bukhari · Sahih Muslim

---

## Features

- **Scholarly AI chat** — grounded strictly in authentic Seerah sources
- **Multi-turn conversations** — full chat history with persistent sessions
- **Authentication** — secure user accounts with NextAuth
- **Chat management** — create, title, and revisit past conversations
- **Source referencing** — responses cite relevant Sirat un Nabi volumes
- **Historical context** — 7th-century Arabian context provided alongside answers

---

## Tech Stack

- **Framework** — Next.js 14 (App Router)
- **AI** — Anthropic Claude API (`@anthropic-ai/sdk`)
- **Auth** — NextAuth v4 with Prisma adapter
- **Database** — PostgreSQL via Prisma ORM
- **Hosting** — Supabase (database) + Vercel (app)
- **Styling** — Tailwind CSS

---

## Architecture

```
src/
├── app/
│   ├── (auth)/
│   │   ├── login/         # Login page
│   │   └── register/      # Registration page
│   ├── api/
│   │   ├── auth/          # NextAuth handlers
│   │   └── chats/         # Chat & message API routes
│   ├── chat/              # Main chat interface
│   └── timeline/          # Seerah timeline view
├── lib/
│   ├── seerah-prompt.ts   # Core system prompt grounded in Sirat un Nabi
│   ├── auth.ts            # NextAuth config
│   └── prisma.ts          # Prisma client
├── components/
│   └── Providers.tsx      # Session provider wrapper
prisma/
└── schema.prisma          # User, Chat, Message models
```

---

## Local Setup

```bash
# Clone the repo
git clone https://github.com/younassadat/seerah-companion
cd seerah-companion

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Fill in: DATABASE_URL, NEXTAUTH_SECRET, NEXTAUTH_URL, ANTHROPIC_API_KEY

# Push database schema
npx prisma db push

# Run development server
npm run dev
```

---

## Guiding Principles

- Responses always write ﷺ (saw) after the Prophet's name and (RA) after companions
- No fatwas — focus is strictly on historical biography and scholarship
- Misconceptions addressed calmly with scholarly depth and primary source references
- Built with deep respect for Islamic scholarship and the integrity of the Seerah

---

*Built by [Younas Sadat](https://github.com/younassadat) · Islamabad, Pakistan*
