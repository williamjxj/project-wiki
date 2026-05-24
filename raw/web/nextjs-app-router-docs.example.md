---
type: web-article
source: web
topic: "Next.js App Router documentation"
date: 2026-05-24
status: pending
url: "https://nextjs.org/docs/app"
---

# Next.js App Router — Key Concepts

## Server Components

Default in App Router. Components render on the server unless marked `"use client"`.

## Middleware

Runs before routes. Used for auth checks, redirects, and header manipulation. Important for protecting routes and handling session cookies.

## Route Handlers

API endpoints in `app/api/` directory. Replace Pages Router `pages/api/`.

## Relevance to Auth

Middleware is the primary integration point for session-based auth providers (Clerk, Auth0, NextAuth) in App Router apps.
