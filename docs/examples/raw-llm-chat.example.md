---
type: llm-chat
source: claude
topic: "auth patterns for SaaS MVP"
date: 2026-05-24
status: pending
question: "What auth approach should I use for a B2B SaaS MVP built with Next.js?"
---

# Claude — Auth Patterns for SaaS MVP

## Recommendation

Use **Clerk** for a B2B SaaS MVP. Fastest time-to-ship, good Next.js App Router integration, handles org/team features out of the box.

## Key Points

- Don't roll your own auth for an MVP — security mistakes are costly
- JWT + refresh tokens are sufficient for API auth once users are authenticated via Clerk
- Watch out for SSR cookie handling with Next.js App Router middleware
- Auth0 is powerful but overkill for early-stage MVPs (complex pricing, steep setup)

## Alternatives Mentioned

- **NextAuth**: Good if self-hosting is required, but more setup than Clerk
- **Supabase Auth**: Viable if already using Supabase for database
- **Auth0**: Enterprise-grade but heavy for MVP stage
