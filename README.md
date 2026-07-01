<div align="center">
  <br />
  <img src="public/readme/readme-hero.webp" alt="FlowMind Banner">
  <br />

  <div>

<img src="https://img.shields.io/badge/-Next.js-black?style=for-the-badge&logo=nextdotjs&logoColor=white" />
<img src="https://img.shields.io/badge/-Typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/-Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" />
<img src="https://img.shields.io/badge/-shadcn/ui-000000?style=for-the-badge&logo=shadcnui&logoColor=white" /><br/>

<img src="https://img.shields.io/badge/-Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white" />
<img src="https://img.shields.io/badge/-PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white" />
<img src="https://img.shields.io/badge/-Clerk-6C47FF?style=for-the-badge&logo=clerk&logoColor=white" /><br/>

<img src="https://img.shields.io/badge/Trigger.dev-22c55e?style=for-the-badge&logo=triggerdotdev&logoColor=white" />
<img src="https://img.shields.io/badge/-Liveblocks-050505?style=for-the-badge&logo=liveblocks&logoColor=white" />

  </div>

  <h3 align="center">FlowMind — AI-Powered Collaborative System Design</h3>

</div>

## 📋 Table of Contents

1. ✨ [Introduction](#introduction)
2. ⚙️ [Tech Stack](#tech-stack)
3. 🔋 [Features](#features)
4. 🤸 [Quick Start](#quick-start)

## <a name="introduction">✨ Introduction</a>

FlowMind is an agentic system design workspace built for software teams. Submit a natural-language prompt (e.g., "Design a scalable e-commerce backend") and a Google Gemini-powered AI agent autonomously places nodes and edges onto a shared React Flow canvas in real-time. Teammates can watch the AI build the diagram live, then jump in to collaboratively refine it. Once the team is satisfied, a second AI background task converts the visual graph into a comprehensive, multi-page Markdown technical specification that can be downloaded directly from the app.

## <a name="tech-stack">⚙️ Tech Stack</a>

- **[Next.js](https://nextjs.org/)** — Full-stack React framework with server-side rendering, API routes, and App Router.
- **[TypeScript](https://www.typescriptlang.org/)** — Static typing for safer, more maintainable code.
- **[Liveblocks](https://liveblocks.io/)** — Real-time collaboration infrastructure: synchronized canvas state, live cursors, and presence.
- **[Clerk](https://clerk.com/)** — Authentication and user management with drop-in components for Next.js.
- **[Trigger.dev](https://trigger.dev/)** — Durable background tasks for long-running AI agent jobs.
- **[Prisma ORM](https://www.prisma.io/)** — Type-safe database client generated from your schema.
- **[PostgreSQL](https://www.postgresql.org/)** — Persistent storage for projects and spec metadata.
- **[Tailwind CSS](https://tailwindcss.com/)** — Utility-first CSS with full light/dark mode support.
- **[shadcn/ui](https://ui.shadcn.com/)** — Accessible, composable UI components built on Radix UI.
- **[Google Gemini](https://aistudio.google.com/)** — AI model powering canvas generation and spec writing.

## <a name="features">🔋 Features</a>

- **AI Architecture Agent** — Submit a plain-English prompt; Gemini draws nodes and edges onto the live canvas in real-time via Trigger.dev background tasks and the Liveblocks Node.js SDK.
- **Multiplayer Canvas** — Full real-time collaboration: synchronized node/edge state, live cursor positions, and presence avatars for every connected user.
- **Custom Canvas Nodes** — Double-click to edit labels inline; resize with NodeResizer; choose from 8 colour swatches via a floating NodeToolbar — all synced instantly.
- **AI Spec Generation** — One click converts the current graph into a detailed Markdown technical specification.
- **Downloadable Specs** — Every generated spec is available via a dedicated download route.
- **Light / Dark Mode** — Theme-aware UI with flash-prevention; toggle persists across sessions.
- **Clerk Authentication** — Global route protection; Liveblocks tokens only issued to authenticated users.
- **Auto-Save Canvas** — Canvas state debounce-saved to Vercel Blob every 3 seconds of inactivity.
- **Project Management** — Create projects from a slide-in sidebar; project slugs auto-generate room IDs.

## <a name="quick-start">🤸 Quick Start</a>

**Prerequisites**

- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en)
- [npm](https://www.npmjs.com/)

**Clone the Repository**

```bash
git clone https://github.com/khrisdain/ghost-ai.git
cd ghost-ai
```

**Install Dependencies**

```bash
npm install
```

**Set Up Environment Variables**

Create a `.env` file in the project root:

```env
# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up

# Liveblocks
LIVEBLOCKS_SECRET_KEY=

# Trigger.dev
TRIGGER_SECRET_KEY=
TRIGGER_PROJECT_REF=

# Database (Prisma Postgres)
DATABASE_URL=

# Google AI
GOOGLE_AI_API_KEY=

# Vercel Blob
BLOB_READ_WRITE_TOKEN=
BLOB_STORE_ID=
```

**Run the App**

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

**Run Trigger.dev (Background AI Tasks)**

In a second terminal:

```bash
npx trigger.dev@latest dev
```

## Available Scripts

| Command                   | Description                           |
| ------------------------- | ------------------------------------- |
| `npm run dev`             | Start Next.js development server      |
| `npm run build`           | Build for production                  |
| `npm run start`           | Start production server               |
| `npm run lint`            | Run ESLint                            |
| `npm run prisma:generate` | Regenerate Prisma client              |
| `npm run prisma:migrate`  | Create and apply a new migration      |
| `npm run prisma:deploy`   | Apply pending migrations (production) |
| `npm run prisma:studio`   | Open Prisma Studio GUI                |

## Project Structure

```
.
├── app/
│   ├── api/              # Next.js API routes (auth, AI, projects, specs)
│   ├── editor/           # Canvas editor pages
│   ├── sign-in/          # Clerk sign-in page
│   └── sign-up/          # Clerk sign-up page
├── components/
│   ├── editor/           # Canvas UI (editor, sidebar, AI chat, nodes, edges)
│   └── ui/               # shadcn/ui primitives
├── hooks/                # Custom React hooks (auto-save, keyboard shortcuts)
├── lib/                  # Shared utilities (Prisma, Liveblocks, theme)
├── prisma/               # Schema and migrations
├── trigger/              # Trigger.dev background tasks
│   ├── design-agent.ts   # AI canvas generation
│   └── generate-spec.ts  # AI spec generation
└── types/                # Shared TypeScript types
```
