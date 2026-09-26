# WVSTU Digital Campus

A prototype "unified student, academic & university services platform" for
William V. S. Tubman University (WVSTU), Liberia. This is a demonstration
project — it is not an official WVSTU system.

## What's here

This repo contains a single self-contained static site:

- `index.html` — the entire application (public site, Student Portal,
  Faculty Portal, Administration dashboard). No build step, no dependencies
  to install — it's plain HTML/CSS/JavaScript plus the Supabase JS client
  loaded from a CDN.
- `vercel.json` — tells Vercel to serve `index.html` for every URL path
  (`/`, `/admin`, `/faculty`, etc.), since this is a single-page app that
  reads the current path in JavaScript to decide which login screen to show.

## How it's wired together

- **Frontend:** this repo, deployed on Vercel.
- **Backend:** Supabase (Postgres + Auth + Storage), project ref
  `nvglypbkvxdpizxtdlnu`. All business rules (GPA-based credit-load caps,
  75% tuition-clearance gate, document-request limits, etc.) are enforced
  in the database itself via Row Level Security policies and triggers —
  not just in the JavaScript, so they can't be bypassed by editing the page.

## Demo accounts

| Role    | Login                      | Password      | Access via         |
|---------|-----------------------------|---------------|---------------------|
| Student | username `jamesdoe`         | `Doe@2026`    | the homepage (`/`)  |
| Faculty | `dr.nyema@wvstu.edu.lr`     | `FACULTY2026` | `/faculty`          |
| Admin   | `admin@wvstu.edu.lr`        | `ADMIN2026`   | `/admin`            |

Faculty and Admin logins are intentionally **not** shown anywhere on the
public homepage — they only appear if you go directly to `/faculty` or
`/admin`.

## Updating this site

1. Edit `index.html` (or ask Claude to prepare an updated version).
2. Upload the new file to this repo, replacing the old one (GitHub's
   "Add file → Upload files" screen, or drag-and-drop onto the repo page).
3. Commit the change.
4. Vercel is connected to this repo and will automatically redeploy within
   about 30 seconds of the commit — no manual redeploy step needed once the
   first deployment is set up.

## Known scope notes (intentional, not bugs)

- Photo backgrounds (crest logo, graduation photo) were removed from this
  build to keep the file small enough to upload/transfer easily. They can
  be added back by hosting the images in Supabase Storage and referencing
  the public URLs in the CSS, rather than embedding them as base64 data.
- Bulk student import and admissions document upload are UI-complete but
  not wired to live writes yet — both need a small secure server-side
  piece (a Supabase Edge Function) since they require privileges that
  must never sit in browser-side code.
