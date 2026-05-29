# INSTRUCTIONS_CODING.md
# Technical Setup: GitHub Org, Deployment & Code Structure
### Professor Aakash Tyagi — Personal Webpage

---

## 1. PROJECT FILE STRUCTURE

```
tyagi-tamu.github.io/
│
├── index.html                ← Main website (design shell — do not edit)
│
├── data/
│   ├── sections.json         ← Master config: show/hide/reorder sections
│   ├── profile.json          ← Name, bio, contact, education, links
│   ├── research.json         ← Research area cards
│   ├── news.json             ← Lab news items
│   ├── publications.json     ← All papers with links
│   ├── awards.json           ← Awards and honors
│   ├── students.json         ← Current students and alumni
│   └── teaching.json         ← Courses taught
│
└── assets/
    ├── img/
    │   └── tyagi.jpg         ← Professor's photo (replace with new photo anytime)
    └── css/                  ← (reserved for future style overrides)
```

---

## 2. CREATE THE GITHUB ORGANIZATION

**Step 1:** Go to https://github.com and sign in (or create an account).

**Step 2:** Click your profile picture (top right) → **"Your organizations"** → **"New organization"**.

**Step 3:** Choose the **Free** plan.

**Step 4:** Set the organization name to: `tyagi-tamu`
- This makes the site URL: `https://tyagi-tamu.github.io`

**Step 5:** Enter your email. Skip adding members for now. Click **"Complete setup"**.

**Step 6:** Invite the professor as an **Owner**:
- Go to `github.com/tyagi-tamu` → Settings → Members → Invite by email.

---

## 3. CREATE THE REPOSITORY

**Step 1:** Inside the `tyagi-tamu` organization, click **"New repository"**.

**Step 2:** Name it **exactly**: `tyagi-tamu.github.io`
> ⚠️ The repo name MUST match the org name + `.github.io` — this is what activates GitHub Pages.

**Step 3:** Set it to **Public**.

**Step 4:** Do NOT initialize with README. Click **"Create repository"**.

---

## 4. UPLOAD ALL FILES

**Step 1:** On the empty repo page, click **"uploading an existing file"** link.

**Step 2:** Drag and drop ALL project files maintaining the folder structure:
- `index.html`
- `data/sections.json`
- `data/profile.json`
- `data/research.json`
- `data/news.json`
- `data/publications.json`
- `data/awards.json`
- `data/students.json`
- `data/teaching.json`
- `assets/img/tyagi.jpg`

**Step 3:** Scroll down, write commit message: `Initial site upload`

**Step 4:** Click **"Commit changes"**.

> 💡 GitHub does not allow uploading empty folders. Upload all files with their paths and GitHub will create the folders automatically. You can also create folders by typing `data/` before the filename when GitHub asks for a file path.

---

## 5. ENABLE GITHUB PAGES

**Step 1:** In the repository, click **"Settings"** (top menu).

**Step 2:** In the left sidebar, click **"Pages"**.

**Step 3:** Under **Source**, select:
- Branch: `main`
- Folder: `/ (root)`

**Step 4:** Click **"Save"**.

**Step 5:** Wait 60–90 seconds. Refresh the page. You will see:
> ✅ "Your site is live at https://tyagi-tamu.github.io"

---

## 6. ADD THE PROFESSOR'S PHOTO

The photo was not downloadable automatically due to TAMU server restrictions.

**Option A — Download manually:**
1. Go to: `https://engineering.tamu.edu/cse/profiles/tyagi-aakash.html`
2. Right-click the professor's photo → **"Save image as"**
3. Save as `tyagi.jpg`
4. Upload it to `assets/img/tyagi.jpg` in the GitHub repo

**Option B — Use any photo:**
1. Save it as `tyagi.jpg`
2. Upload to `assets/img/tyagi.jpg`
3. The site will automatically display it in the hero section

> 📝 If no photo is uploaded, the site gracefully shows "AT" initials placeholder — it won't break.

---

## 7. CHANGING THE SITE NAME LATER

If you ever want to rename from `tyagi-tamu` to something else (e.g. `aakashtyagi`):

**Step 1:** Go to GitHub Org Settings → rename org to `aakashtyagi`

**Step 2:** Rename the repo from `tyagi-tamu.github.io` to `aakashtyagi.github.io`

**Step 3:** In `data/profile.json`, update the `tamu_profile` field if needed.

**That's it.** GitHub auto-redirects the old URL. No other files need changing.

---

## 8. SETTING UP A CUSTOM DOMAIN (OPTIONAL)

If the professor wants a domain like `aakashtyagi.com`:

**Step 1:** Buy the domain from any registrar (Namecheap, Google Domains, etc.).

**Step 2:** In your domain registrar's DNS settings, add these records:
```
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
CNAME www   tyagi-tamu.github.io
```

**Step 3:** In GitHub repo → Settings → Pages → **Custom domain** → type `aakashtyagi.com` → Save.

**Step 4:** Check **"Enforce HTTPS"** checkbox.

Wait up to 24 hours for DNS to propagate. Site will then be live at `https://aakashtyagi.com`.

---

## 9. HOW THE CODE WORKS (FOR FUTURE DEVELOPERS)

The site has **zero build steps**. It is plain HTML + JavaScript.

### How sections load:
1. `index.html` loads on browser open
2. JavaScript reads `data/sections.json` to know which sections are enabled
3. For each enabled section, it fetches the corresponding JSON file
4. It renders the data into the page using template functions

### Adding a completely new section (e.g. "Grants"):
1. Create `data/grants.json` with your data structure
2. Add an entry to `data/sections.json`:
   ```json
   { "id": "grants", "title": "Grants", "file": "grants.json", "enabled": true }
   ```
3. Open `index.html`, find the comment `// ── SECTION RENDERER MAP` (~line 295)
4. Add a case inside the `switch` statement:
   ```javascript
   case 'grants': return renderGrants(allData.grants);
   ```
5. Add your `renderGrants(data)` function above the switch (follow the pattern of existing functions)
6. Add `grants` to the `Promise.all` array and the `allData` object at the bottom

### Fonts used:
- **Cormorant Garamond** — headings, names, year labels (Google Fonts)
- **DM Sans** — body text, navigation, metadata

### Color variables (in CSS `:root`):
```css
--maroon:      #500000   /* TAMU maroon — primary accent */
--maroon-light:#7a1c1c   /* hover states */
--maroon-pale: #f9f1f1   /* light maroon backgrounds */
--cream:       #fdfaf7   /* page background */
--accent:      #c8a96e   /* gold decorative border on photo */
```

---

## 10. TESTING LOCALLY

Because the site fetches JSON files, you cannot open `index.html` directly by double-clicking it (browsers block local file fetches for security).

**Use Python (easiest):**
```bash
cd tyagi-tamu
python3 -m http.server 8000
```
Then open: `http://localhost:8000`

**Use Node.js:**
```bash
npx serve .
```

**VS Code users:** Install the **Live Server** extension → right-click `index.html` → "Open with Live Server"

---

## 11. AFTER EVERY EDIT

Every time you or the professor edits any file on GitHub:
- Click the ✏️ pencil icon on the file
- Make the change
- Scroll down → click **"Commit changes"**
- The live site updates automatically within **60 seconds**

No build. No deploy command. No terminal needed.
