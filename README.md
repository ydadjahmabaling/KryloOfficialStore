# Krylo Market

A dynamic Roblox gaming store — **Krylo Market** — with a glitch intro animation
("go with gaming?" → *gaming* glitches into **Krylo**), USD pricing, user & admin
login, admin item listings with thumbnail uploads, and a built-in message system.

## Features
- **Glitch intro** — plays once per tab session; refreshes don't replay it (sessionStorage).
- **Accounts** — register / login with scrypt-hashed passwords, HMAC cookie sessions.
- **Admin panel** (`#/admin`) — post items for sale: name, USD price, description,
  thumbnail via image upload (base64) or URL. Delete listings.
- **Store** — searchable item grid, item detail pages, all prices in **USD**.
- **Message system** — "Contact Seller" on any item opens a conversation;
  threaded inbox with unread badges and replies (for buyers AND sellers).
- **Database** — zero-dependency JSON database (seeded with an admin account and demo items).

## Run locally
```bash
node server.js        # → http://localhost:3000
```

## Deploy on Vercel
1. Push this folder to GitHub/GitLab and **Import** it in Vercel (framework: *Other*).
   Vercel auto-detects the `api/` serverless functions — no config needed.
2. Or run: `npx vercel`

### Default admin account
| Email | Password |
|---|---|
| `admin@krylo.market` | `admin123` |

Override at first launch with env vars: `ADMIN_EMAIL`, `ADMIN_PASSWORD`, `KRYLO_SECRET`.

## Important: data persistence on Vercel
Vercel serverless filesystems are **ephemeral** — the JSON database resets when a
function instance restarts. For a hobby/demo deploy this works, but for real
persistent data use one of:
- `KRYLO_DATA_DIR` env var pointing at persistent storage, **or**
- Swap `api/lib/db.js` for Vercel Postgres / Neon / Supabase (keep the same exported
  function signatures and nothing else changes).

## Files
```
index.html  style.css  app.js  logo.png   ← frontend (logo.png = site logo)
server.js                                  ← local dev server
api/                                       ← Vercel serverless API
  register.js login.js logout.js me.js
  items.js  items/[id].js                  ← listings CRUD (admin writes)
  messages.js                              ← inbox / send / mark-read
  lib/ db.js auth.js http.js               ← JSON DB + scrypt/HMAC auth
```
