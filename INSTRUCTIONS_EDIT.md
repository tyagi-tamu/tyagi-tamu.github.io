# INSTRUCTIONS_EDIT.md
# How to Edit the Website
### Professor Aakash Tyagi — Personal Webpage
### For: Professor Tyagi and students maintaining the site

---

> **Golden Rule:** You will NEVER need to touch `index.html`.
> All edits happen in the `data/` folder only.

---

## HOW TO EDIT ANY FILE ON GITHUB

Every edit follows the same 4 steps:

1. Go to `github.com/tyagi-tamu/tyagi-tamu.github.io`
2. Click on the file you want to edit (e.g. `data/awards.json`)
3. Click the **pencil icon ✏️** (top right of file view)
4. Make your change → scroll down → click **"Commit changes"** → click **"Commit changes"** again

✅ Site updates live within **60 seconds**. That's it.

---

## SECTION 1 — Show, Hide, or Reorder Sections

**File to edit:** `data/sections.json`

### To HIDE a section (e.g. hide Teaching temporarily):
Find the section and change `"enabled": true` to `"enabled": false`

```json
{ "id": "teaching", "title": "Teaching", "file": "teaching.json", "enabled": false }
```

### To SHOW it again:
Change back to `"enabled": true`

### To REORDER sections:
Cut and paste the entire line to a new position. The page renders sections in the order they appear here.

**Example — move News above Research:**
```json
[
  { "id": "about",        ... "enabled": true },
  { "id": "news",         ... "enabled": true },
  { "id": "research",     ... "enabled": true },
  ...
]
```

---

## SECTION 2 — Update Bio, Contact, or Education

**File to edit:** `data/profile.json`

### Update bio paragraphs:
Find the `"bio"` section. Each `"..."` is one paragraph. Edit the text inside the quotes.
```json
"bio": [
  "First paragraph text here...",
  "Second paragraph text here...",
  "Third paragraph text here..."
]
```
To add a new paragraph, add a new line:
```json
"bio": [
  "Existing paragraph...",
  "Existing paragraph...",
  "New paragraph you are adding now."
]
```

### Update contact info:
```json
"email": "tyagi@cse.tamu.edu",
"phone": "979-845-5480",
"office": "PETR 207"
```
Just change the value inside the quotes.

### Add a new degree to Education:
```json
{
  "degree": "Ph.D.",
  "field": "Your Field",
  "institution": "University Name",
  "location": "City, State",
  "year": "2000"
}
```
Add a comma after the last `}` in the list, then paste this block.

---

## SECTION 3 — Add or Edit a Publication

**File to edit:** `data/publications.json`

### Add a new paper (add to the TOP of the file, after the opening `[`):
```json
{
  "year": 2026,
  "title": "Your Paper Title Here",
  "authors": "A. Tyagi, J. Hu, et al.",
  "venue": "Conference or Journal Name",
  "month": "Month Year",
  "link": "https://doi-or-arxiv-link-here"
}
```

> ⚠️ After the `}`, add a comma `,` before the next entry. The LAST entry has no comma.

### Edit an existing paper:
Find it by title, click ✏️, change what you need.

### Remove a paper:
Delete the entire block from `{` to `}` including the trailing comma.

---

## SECTION 4 — Add or Edit an Award

**File to edit:** `data/awards.json`

### Add a new award (add to the TOP for most recent first):
```json
{
  "year": 2025,
  "title": "Full Award Name Here",
  "org": "Awarding Organization"
}
```

### Example — a real entry:
```json
{
  "year": 2024,
  "title": "Texas A&M Association of Former Students University-Level Distinguished Achievement Award for Individual Student Engagement",
  "org": "Texas A&M University"
}
```

---

## SECTION 5 — Add or Edit a News Item

**File to edit:** `data/news.json`

### Add a news item (add to the TOP for most recent first):
```json
{
  "date": "Month Year",
  "title": "News headline here",
  "description": "One or two sentences describing the news.",
  "link": "https://link-to-full-article-or-leave-empty-string"
}
```

### To add news without a link:
```json
{
  "date": "January 2026",
  "title": "Paper accepted at ICCAD 2026",
  "description": "Congratulations to the team on the paper acceptance.",
  "link": ""
}
```

---

## SECTION 6 — Add or Edit a Student

**File to edit:** `data/students.json`

The file has two sections: `"current"` and `"alumni"`.

### Add a current student:
```json
{
  "name": "Student Full Name",
  "degree": "PhD",
  "photo": ""
}
```
For `"degree"`, use: `"PhD"`, `"MS"`, `"BS"`, or `"Postdoc"`

### Graduate a student (move from current to alumni):
1. Remove from the `"current"` list
2. Add to the `"alumni"` list:
```json
{
  "name": "Student Full Name",
  "degree": "PhD 2026",
  "current_position": "Google, Inc.",
  "photo": ""
}
```

### Add a student photo:
1. Upload the photo to `assets/img/` in the GitHub repo (name it e.g. `john-doe.jpg`)
2. Set `"photo": "assets/img/john-doe.jpg"` in students.json

> If `"photo"` is left empty `""`, the site shows the student's initials automatically — it won't break.

---

## SECTION 7 — Add or Edit a Course

**File to edit:** `data/teaching.json`

### Add a course:
```json
{
  "name": "Machine Learning for Hardware Design",
  "level": "Graduate",
  "notes": "New course starting Spring 2026"
}
```

For `"level"`, use: `"Undergraduate"`, `"Graduate"`, or `"Undergraduate / Graduate"`

---

## SECTION 8 — Add or Edit a Research Area

**File to edit:** `data/research.json`

### Add a new research area:
```json
{
  "title": "Security Verification",
  "description": "One to two sentences describing this research area and what the lab is working on.",
  "icon": "chip"
}
```

For `"icon"`, use any of: `"chip"`, `"cpu"`, `"brain"`, `"code"`

---

## SECTION 9 — Replace the Professor's Photo

1. Save the new photo as `tyagi.jpg` (exact name, lowercase)
2. In GitHub, go to `assets/img/`
3. Click **"Add file"** → **"Upload files"**
4. Upload `tyagi.jpg` — it will replace the existing one
5. Commit changes → photo updates on site within 60 seconds

---

## SECTION 10 — Add a Brand New Section (e.g. Grants, Talks, Press)

This requires a small code change. Follow these 3 steps:

### Step 1 — Create the data file
Create `data/grants.json` with your content. Example:
```json
[
  {
    "year": 2025,
    "title": "NSTC/Natcast Workforce Development Grant",
    "amount": "$1.28M",
    "agency": "US Department of Commerce",
    "description": "WAVE-CHIP program for hardware verification workforce development."
  }
]
```

### Step 2 — Register it in sections.json
Add a line to `data/sections.json`:
```json
{ "id": "grants", "title": "Grants & Funding", "file": "grants.json", "enabled": true }
```

### Step 3 — Add renderer in index.html
Open `index.html`, find the comment line:
```
// ── SECTION RENDERER MAP
```
Add a `case` inside the switch:
```javascript
case 'grants': return renderGrants(allData.grants);
```
Then add the `renderGrants` function above it (copy the pattern of `renderAwards`).
Also add `grants` to the `Promise.all` array and `allData` object at the bottom of the script.

> 💡 If you're not comfortable editing `index.html`, ask the student who built the site — Steps 1 and 2 can be done by anyone, and Step 3 takes about 10 minutes for a developer.

---

## QUICK REFERENCE CHEAT SHEET

| I want to...                     | File to edit               | Where in file         |
|----------------------------------|----------------------------|-----------------------|
| Update bio                       | `data/profile.json`        | `"bio"` array         |
| Change email / phone / office    | `data/profile.json`        | top fields            |
| Add a publication                | `data/publications.json`   | top of list           |
| Add an award                     | `data/awards.json`         | top of list           |
| Add a news item                  | `data/news.json`           | top of list           |
| Add a current student            | `data/students.json`       | `"current"` array     |
| Graduate a student to alumni     | `data/students.json`       | move to `"alumni"`    |
| Add a course                     | `data/teaching.json`       | anywhere in list      |
| Add a research area              | `data/research.json`       | anywhere in list      |
| Hide a section temporarily       | `data/sections.json`       | `"enabled": false`    |
| Reorder sections on page         | `data/sections.json`       | reorder the lines     |
| Replace professor photo          | `assets/img/tyagi.jpg`     | upload new file       |

---

## COMMON MISTAKES TO AVOID

**❌ Missing comma between entries:**
```json
{ "year": 2024, "title": "Award A" }   ← missing comma here
{ "year": 2023, "title": "Award B" }
```
✅ Should be:
```json
{ "year": 2024, "title": "Award A" },
{ "year": 2023, "title": "Award B" }
```

**❌ The LAST entry should NOT have a comma:**
```json
{ "year": 2022, "title": "Award C" }   ← no comma on last item ✅
```

**❌ Forgetting quotes around text values:**
```json
"year": 2024        ← numbers: no quotes needed ✅
"title": Award A    ← text: MUST have quotes ❌
"title": "Award A"  ← correct ✅
```

**❌ Using straight apostrophes in text that might conflict:**
If you need an apostrophe in a title, it's fine: `"title": "Texas A&M's Award"`

---

## IF THE SITE LOOKS BROKEN

1. Go to the GitHub repo
2. Click on **"Actions"** tab — you'll see if any commit caused an error
3. Most likely a JSON syntax error (missing comma, missing quote)
4. Use https://jsonlint.com — paste your JSON, click Validate, it will show the exact line with the error
5. Fix it, commit, site restores in 60 seconds
