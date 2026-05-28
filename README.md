# Jyory — Digital Business Cards (NFC)

A free, single-file digital business card system (Blinq-style) for Jyory.
Open `index.html` in any browser to preview it locally.

## What it does

- **2 cards in one file** — *Akshay* (personal) and *Jyory Store* (brand),
  switched by the pills at the top. Each card has its own link:
  `index.html?card=akshay` and `index.html?card=store` (up to 5 supported).
- **Save Contact** — one tap downloads a vCard with all details.
- **Exchange Contact** — a lead-capture form; submissions open a pre-filled
  WhatsApp message to **+91 80008 38898** so you receive the lead instantly.
- **Branded QR code** — auto-generated, points to the current card, in your
  navy/gold colours. Download it or copy the link.
- **Light / dark theme toggle** — sun/moon button, remembers the choice.
- **Quick actions + social links** — Call, WhatsApp, Email, Website, Instagram,
  LinkedIn, GitHub, Location, and more.

---

## How to edit

Open `index.html` in Notepad / VS Code. There are **two blocks** at the top:

### 1. `SETTINGS` — shared across all cards

| What to change          | Key                                              |
| ----------------------- | ------------------------------------------------ |
| Which card shows first  | `defaultCard: "akshay"`                          |
| Default theme           | `defaultTheme: "dark"` / `"light"`               |
| Where leads are sent    | `leadWhatsApp` (country code + number, **no +**) |
| Live URL for QR/Share   | `publicUrl` (set after deploy, or leave blank)   |
| QR colours              | `qr: { dark, light }` (hex **without** `#`)      |
| Theme colours           | `themes.dark.*`, `themes.light.*`                |

> **Important after deploying:** set `publicUrl` to your live address, e.g.
> `publicUrl: "https://aks2495.github.io/jyory-card/"`. This makes the QR code
> and Share button point to the real site instead of a local file path.

### 2. `CARDS` — one entry per card

Each card has: `tabLabel`, `logo`, `fullName`, `firstName`, `lastName`,
`title`, `company`, `tagline`, `location`, `about`, `phone`, `whatsapp`,
`email`, `website`, and a `links: [ ... ]` array.

- **Edit a card:** change any value and save.
- **Add a card (up to 5):** copy a whole `akshay: { ... }` block, give it a new
  key (e.g. `sales: { ... }`), edit the details. A new pill appears automatically.
- **Remove a card:** delete its block.

To add a social link, copy any line in a `links` array and change the fields.
Supported `type` values (each has a matching icon):

```
whatsapp · phone · email · website · instagram · linkedin · github
location · youtube · facebook · twitter · pinterest · custom
```

(`twitter` uses the new X logo.) Each card's `links` already includes commented-
out examples for YouTube, Facebook, Pinterest, and X — uncomment and add URLs.

### Adding your logo

1. Save the JYORY logo (or any wordmark/horizontal logo) as `logo.png`
   in this same folder. PNG with transparent background looks cleanest,
   but a dark-background PNG also works because the container is navy.
2. The card picks it up automatically.
3. If you'd rather show the built-in SVG JY diamond mark, either delete
   the file or set `logo: ""` in the `CARD` block.

### Theme toggle

A small sun/moon button in the top-right corner switches between **dark** (deep
navy + gold, matches the printed card) and **light** (cream + deep gold). The
visitor's choice is remembered; the default is `SETTINGS.defaultTheme`.

### Lead capture (Exchange Contact)

Tapping **Exchange Contact** opens a form (name, phone, email, message). On
submit it opens WhatsApp with the details pre-filled, addressed to
`SETTINGS.leadWhatsApp`. No server, no database — the lead lands straight in
your WhatsApp chat. Change the destination number in `SETTINGS.leadWhatsApp`.

### QR code

The QR is generated on the fly (via the free api.qrserver.com service) and
points to whatever `publicUrl` you set, plus the active card. It needs an
internet connection to render — fine for a hosted card. **Download QR** saves a
PNG you can print; **Copy Link** copies the card URL.

### Optional: free visitor analytics

Near the top of `index.html` there's a commented-out GoatCounter snippet. Sign
up free at https://www.goatcounter.com, uncomment the line, drop in your code,
and you'll see how many people open your card. Off by default.

---

## Deploy for free — GitHub Pages (~60 seconds)

Google Drive doesn't host websites anymore (discontinued in 2016), so we'll use
GitHub Pages. You already have a GitHub account (`Aks2495`), so this is free
and instant.

### Steps

1. Go to https://github.com/new
2. Repository name: `jyory-card`  →  set **Public**  →  **Create repository**
3. On the new repo page, click **uploading an existing file**
4. Drag `index.html` into the upload box  →  **Commit changes**
5. Go to **Settings → Pages** (left sidebar)
6. Under **Source**, choose **Deploy from a branch**
7. Branch: `main`, Folder: `/ (root)`  →  **Save**
8. Wait ~30 seconds. Your card is live at:

   ```
   https://aks2495.github.io/jyory-card/
   ```

### Put it on your NFC tag

1. Install **NFC Tools** (free, iOS/Android)
2. **Write → Add a record → URL/URI**
3. Paste your GitHub Pages URL → **Write** → tap your NFC card

Done. Anyone who taps the card opens your profile instantly.

### Updating later

After the first deploy, just edit `index.html` on your computer, then on the
GitHub repo page click **Add file → Upload files**, drop the new `index.html`,
and commit. Changes are live in ~30 seconds. The NFC tag never needs to be
re-written — the URL stays the same.

---

## Other free hosting options (if you don't want GitHub)

- **Netlify Drop** — https://app.netlify.com/drop — drag the folder, get a URL. No account needed for the first deploy.
- **Cloudflare Pages** — free, fast, custom domain support.
- **Vercel** — free, similar to Netlify.

All of them work the same way for a single-file site.

---

## Files

- `index.html` — the entire card. No build step, no dependencies.
- `README.md`  — this file.
