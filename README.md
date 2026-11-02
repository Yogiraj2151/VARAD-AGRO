# Varad Agro Industries — Vercel + Supabase

This is a Vite-powered HTML/CSS/JavaScript app. Supabase configuration is read from environment variables during the Vite build.

## Environment variables
Create a local `.env` file by copying `.env.example`, then set:

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT_REF.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY
```

For Vercel, open **Project → Settings → Environment Variables** and add the same two names and values. Select the environments you need (Production, Preview, Development), save, then redeploy. Vercel does not automatically read a local `.env` file from your computer; set the variables in its dashboard.

`VITE_` variables are included in browser code at build time. Use only the Supabase **publishable** key (`sb_publishable_...`) or legacy **anon** public key. Never use `sb_secret_...` or `service_role`. Keep Row Level Security (RLS) enabled and review policies carefully.

## Deploy
1. Push this folder to GitHub. Do not commit `.env`; `.gitignore` excludes it.
2. Import the repository in Vercel.
3. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` in Vercel Settings → Environment Variables.
4. Build command: `npm run build`; output directory: `dist` (configured in `vercel.json`).
5. Redeploy after adding/changing environment variables.
6. In Supabase → Authentication → URL Configuration, add your deployed Vercel URL to Site URL / Redirect URLs.

## Local development
```bash
cp .env.example .env
npm install
npm run dev
```
On Windows, copy `.env.example` to `.env` using File Explorer or `copy .env.example .env` in Command Prompt. Replace the placeholder values first.

## Database
The frontend expects the existing `public.land_records` table with columns `Date`, `Name`, `Place`, `Gunthe`, `Price/Guntha`, `Guntha Total`, `Bags`, `Price/Bag`, `Bag Total`, `Total Price`, `Online`, `Cash`, `Total Paid`, `Balance`, plus `id`. Review `supabase_setup.sql` and existing RLS policies before applying anything. Starter policies may allow every authenticated user to access all records; do not use those policies for multi-tenant isolation.

## Scope note
The diesel tracking page was not present in the supplied source and is not included in this starter.
