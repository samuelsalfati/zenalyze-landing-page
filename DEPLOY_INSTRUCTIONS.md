# Zenalyze — Replace Framer Site with These Files

## Files to deploy
- `index_final.html` → your main consumer page
- `therapists_final.html` → therapist CRM page

---

## Option A — Vercel (RECOMMENDED — free, 2 minutes)

Vercel is better than GoDaddy for static HTML. You keep your GoDaddy domain,
just point it to Vercel.

### Step 1: Deploy to Vercel
1. Go to https://vercel.com → sign up free (use GitHub or email)
2. Click **"Add New Project"** → choose **"Deploy from template"** → skip
3. Drag and drop BOTH files into the deploy zone
   OR use Vercel CLI: `npx vercel --prod`
4. Vercel gives you a URL like `zenalyze.vercel.app` — test it there first

### Step 2: Connect your GoDaddy domain
1. In Vercel → your project → **Settings → Domains**
2. Add your domain: `zenalyze.ai` (or whatever it is)
3. Vercel shows you DNS records to add — copy them
4. Log into GoDaddy → **DNS Settings** for your domain
5. **Delete** existing A records and CNAME records
6. **Add** the records Vercel gave you (usually 2 records)
7. Wait 5–30 minutes → your domain now points to Vercel

---

## Option B — GoDaddy File Manager (direct upload)

### Step 1: Remove Framer
Your Framer site is probably connected via DNS. You need to:
1. Log into Framer → **Project Settings → Custom Domain**
2. **Disconnect** your domain from Framer
3. This frees up the domain

### Step 2: Upload to GoDaddy Hosting
1. Log into GoDaddy → **My Products → Web Hosting → Manage**
2. Click **cPanel** → **File Manager**
3. Open the `public_html` folder
4. **Delete** any existing `index.html`
5. Click **Upload** → upload both files:
   - `index_final.html` → rename to `index.html` after upload
   - `therapists_final.html` → keep name as-is
6. Visit your domain → live immediately

### If GoDaddy shows "Website Builder" not cPanel:
You're on GoDaddy's drag-and-drop builder — it doesn't support raw HTML.
Switch to Vercel (Option A) and just update your GoDaddy DNS.

---

## Option C — Netlify (also free, also excellent)

1. Go to https://netlify.com → sign up
2. Drag BOTH files onto the Netlify deploy zone
3. Get a URL like `zenalyze.netlify.app`
4. Add your custom domain: Site Settings → Domain Management → Add domain
5. Netlify gives you DNS records → update in GoDaddy DNS same as Vercel above

---

## After going live — wire up Google Sheets for signups

Open `index_final.html` in a text editor, find this line:
```
var SHEET='YOUR_APPS_SCRIPT_URL';
```
Replace `YOUR_APPS_SCRIPT_URL` with your Google Apps Script URL.
See `SETUP_GOOGLE_SHEETS.md` for full instructions.

---

## Quick DNS checklist (GoDaddy)

| What to do | Where |
|---|---|
| Log in | account.godaddy.com |
| Find DNS | My Products → Domain → Manage DNS |
| Delete old records | Remove A records pointing to Framer |
| Add Vercel records | Type: A, Value: 76.76.21.21 |
| Add www redirect | Type: CNAME, Name: www, Value: cname.vercel-dns.com |
| Wait | 5–30 minutes for propagation |

---

## File naming on the server

| Your file | Rename to on server |
|---|---|
| `index_final.html` | `index.html` |
| `therapists_final.html` | `therapists.html` (keep as-is) |

The main page must be named `index.html` — browsers load it automatically.
