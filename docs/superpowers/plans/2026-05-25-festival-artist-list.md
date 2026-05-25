# Festival Artist List Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add artist lineup to the festival program page with custom Untitled1-Regular typography

**Architecture:** Self-contained implementation within program/index.html using inline CSS and local font files. Replace "Stay tuned" placeholder with bilingual title and vertical list of 24 artist names.

**Tech Stack:** HTML5, CSS3, @font-face, existing vanilla JavaScript (no changes)

---

## File Structure

**New:**
- `festival/program/fonts/` (directory)
- `festival/program/fonts/Untitled1-Regular.woff2`
- `festival/program/fonts/Untitled1-Regular.woff`
- `festival/program/fonts/Untitled1-Regular.otf`

**Modified:**
- `festival/program/index.html` (lines 240-248 replaced, CSS added in `<style>` after line 145)

---

### Task 1: Create Fonts Directory

**Files:**
- Create: `festival/program/fonts/` (directory)

- [ ] **Step 1: Create the fonts directory**

```bash
mkdir -p festival/program/fonts
```

Expected: Directory created at `festival/program/fonts/`

- [ ] **Step 2: Verify directory exists**

```bash
ls -la festival/program/ | grep fonts
```

Expected output:
```
drwxr-xr-x  2 user  staff   64 May 25 XX:XX fonts
```

- [ ] **Step 3: Commit**

```bash
git add festival/program/fonts/
git commit -m "feat: create fonts directory for program page

Add fonts directory to hold Untitled1-Regular custom font files.

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

---

### Task 2: Copy Font Files

**Files:**
- Create: `festival/program/fonts/Untitled1-Regular.woff2`
- Create: `festival/program/fonts/Untitled1-Regular.woff`
- Create: `festival/program/fonts/Untitled1-Regular.otf`

- [ ] **Step 1: Copy woff2 file**

```bash
cp /Users/marco/Desktop/Archivio/Untitled1-Regular.woff2 festival/program/fonts/
```

Expected: File copied successfully

- [ ] **Step 2: Copy woff file**

```bash
cp /Users/marco/Desktop/Archivio/Untitled1-Regular.woff festival/program/fonts/
```

Expected: File copied successfully

- [ ] **Step 3: Copy otf file**

```bash
cp /Users/marco/Desktop/Archivio/Untitled1-Regular.otf festival/program/fonts/
```

Expected: File copied successfully

- [ ] **Step 4: Verify all files copied**

```bash
ls -lh festival/program/fonts/
```

Expected output showing three files:
```
-rw-r--r--  1 user  staff   221K May 24 16:34 Untitled1-Regular.otf
-rw-r--r--  1 user  staff   114K May 24 16:34 Untitled1-Regular.woff
-rw-r--r--  1 user  staff   111K May 24 16:34 Untitled1-Regular.woff2
```

- [ ] **Step 5: Commit**

```bash
git add festival/program/fonts/
git commit -m "feat: add Untitled1-Regular font files

Add three font format variants for browser compatibility:
- woff2 (modern browsers)
- woff (older browsers)
- otf (fallback)

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

---

### Task 3: Add Font Face Declaration to CSS

**Files:**
- Modify: `festival/program/index.html:145-146` (insert after line 145, before `</style>`)

- [ ] **Step 1: Read current CSS section**

```bash
sed -n '140,146p' festival/program/index.html
```

Expected: Shows closing styles around line 145

- [ ] **Step 2: Add @font-face declaration**

Add this CSS after line 145 (after the closing `}` of `@media` block, before `</style>`):

```css

    /* Font Face Declaration */
    @font-face {
      font-family: 'Untitled1';
      src: url('fonts/Untitled1-Regular.woff2') format('woff2'),
           url('fonts/Untitled1-Regular.woff') format('woff'),
           url('fonts/Untitled1-Regular.otf') format('opentype');
      font-weight: normal;
      font-style: normal;
      font-display: swap;
    }
```

- [ ] **Step 3: Verify CSS was added correctly**

```bash
grep -A 8 "Font Face Declaration" festival/program/index.html
```

Expected: Shows the complete @font-face block

- [ ] **Step 4: Commit**

```bash
git add festival/program/index.html
git commit -m "feat: add @font-face for Untitled1-Regular

Add font-face declaration with three format fallbacks and
font-display: swap for immediate text rendering.

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

---

### Task 4: Add Artist Section CSS Styles

**Files:**
- Modify: `festival/program/index.html:~155` (after @font-face, before `</style>`)

- [ ] **Step 1: Add artists title styles**

Add this CSS after the @font-face declaration:

```css

    /* Artists Section Title */
    .artists-title {
      font-size: 1.2em;
      text-transform: uppercase;
      letter-spacing: 2px;
      margin-bottom: 20px;
      border-bottom: 2px solid #000;
      padding-bottom: 10px;
    }

    /* Artists List Container */
    .artists-list {
      margin-bottom: 30px;
      text-align: center;
    }

    /* Individual Artist Names */
    .artist-name {
      font-family: 'Untitled1', 'Courier New', Courier, monospace;
      font-size: 0.95rem;
      line-height: 1.8;
      color: #333;
    }
```

- [ ] **Step 2: Verify CSS classes added**

```bash
grep -A 3 "Artists Section Title" festival/program/index.html
grep -A 3 "Artists List Container" festival/program/index.html
grep -A 3 "Individual Artist Names" festival/program/index.html
```

Expected: All three CSS blocks present

- [ ] **Step 3: Commit**

```bash
git add festival/program/index.html
git commit -m "style: add CSS for artist list section

Add styles for:
- .artists-title (uppercase, border-bottom)
- .artists-list (centered container)
- .artist-name (Untitled1 font, 0.95rem, 1.8 line-height)

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

---

### Task 5: Replace "Stay Tuned" with Artist List HTML

**Files:**
- Modify: `festival/program/index.html:240-248` (remove .prose div, add artist section)

- [ ] **Step 1: Verify current content**

```bash
sed -n '238,250p' festival/program/index.html
```

Expected: Shows `<hr>` followed by `.prose` div with "Stay tuned"

- [ ] **Step 2: Replace .prose div with artist section**

Remove lines 240-248 (the entire `.prose` div block) and replace with:

```html
<hr>

    <h2 class="artists-title" data-it="Artisti & Performers" data-en="Artists & Performers">
      Artisti & Performers
    </h2>

    <div class="artists-list">
      <div class="artist-name">Alice Flaviana</div>
      <div class="artist-name">Amphibia</div>
      <div class="artist-name">Bassi Gradassi</div>
      <div class="artist-name">Chantssss</div>
      <div class="artist-name">Classical Hooligans</div>
      <div class="artist-name">Carl Ahnebrink (FLEE Project) + Alan Bolumarrli</div>
      <div class="artist-name">Enrico Malatesta</div>
      <div class="artist-name">Flux by Uchina</div>
      <div class="artist-name">Giesse</div>
      <div class="artist-name">Habitat T.P.U.</div>
      <div class="artist-name">Jungla</div>
      <div class="artist-name">Lorenzo Travaglini</div>
      <div class="artist-name">La Messinscena</div>
      <div class="artist-name">Lemethi</div>
      <div class="artist-name">Proxy Bar</div>
      <div class="artist-name">Mira</div>
      <div class="artist-name">Nicolas Gaunin</div>
      <div class="artist-name">Oleno e Matte</div>
      <div class="artist-name">Privato</div>
      <div class="artist-name">Ramzi</div>
      <div class="artist-name">Reptilian Expo</div>
      <div class="artist-name">Señor Service</div>
      <div class="artist-name">Sister Effect</div>
      <div class="artist-name">Yulia Kachan</div>
    </div>
```

- [ ] **Step 3: Verify HTML structure**

```bash
grep -A 2 "artists-title" festival/program/index.html
```

Expected: Shows h2 with bilingual data attributes

```bash
grep -c "artist-name" festival/program/index.html
```

Expected: `24` (one per artist)

- [ ] **Step 4: Verify all artist names present**

```bash
grep "Alice Flaviana" festival/program/index.html
grep "Yulia Kachan" festival/program/index.html
grep "Carl Ahnebrink" festival/program/index.html
```

Expected: All three artists found (first, last, and one with complex name)

- [ ] **Step 5: Commit**

```bash
git add festival/program/index.html
git commit -m "feat: add artist lineup to program page

Replace 'Stay tuned' placeholder with complete artist list:
- Bilingual section title (IT/EN)
- 24 artists in alphabetical order
- Uses Untitled1-Regular custom font

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

---

### Task 6: Visual Testing and Verification

**Files:**
- Test: `festival/program/index.html` (visual inspection in browser)

- [ ] **Step 1: Open page in browser**

```bash
open festival/program/index.html
```

Or navigate to: `file:///Users/marco/Desktop/formulario-code/formulario-frontend/festival/program/index.html`

- [ ] **Step 2: Verify font loaded**

**Check in browser DevTools:**
1. Open DevTools (F12 or Cmd+Opt+I)
2. Go to Network tab
3. Refresh page
4. Filter by "font"

Expected: Three font files loaded (woff2, woff, otf) with status 200

Alternative check - Console:
```javascript
document.fonts.check("1em Untitled1")
```

Expected: `true`

- [ ] **Step 3: Verify visual appearance**

**Checklist:**
- [ ] Horizontal rule visible above "Artisti & Performers" title
- [ ] Title displayed in uppercase with border-bottom
- [ ] 24 artist names listed vertically, centered
- [ ] Artist names using Untitled1 font (visually distinct from Courier New)
- [ ] Proper spacing between artist names (comfortable to read)
- [ ] No "Stay tuned" text visible

- [ ] **Step 4: Test language toggle**

**In browser:**
1. Click "EN" button (top-right)
2. Verify title changes to "Artists & Performers"
3. Click "IT" button
4. Verify title changes back to "Artisti & Performers"
5. Verify artist names remain unchanged in both languages

Expected: Title switches, artist names stay the same

- [ ] **Step 5: Test responsive behavior**

**In browser DevTools:**
1. Toggle device toolbar (Cmd+Shift+M)
2. Test iPhone SE (375px width)
3. Test iPad (768px width)
4. Test Desktop (1920px width)

Expected: List remains centered and readable at all widths

- [ ] **Step 6: Verify against success criteria**

From spec `docs/superpowers/specs/2026-05-25-artist-list-design.md`:

- [ ] All 24 artist names visible in alphabetical order
- [ ] Untitled1-Regular font applied to artist names
- [ ] Title switches between IT and EN when language toggled
- [ ] Visual consistency with existing page design
- [ ] Font loads with appropriate fallbacks
- [ ] Page remains performant
- [ ] Mobile responsive

---

## Implementation Complete

Once all tasks are complete and visual testing passes, the implementation is done. The program page now displays the full artist lineup with custom typography.

**Final verification:**
```bash
git log --oneline -6
```

Expected: Six commits for this feature (fonts dir, font files, @font-face, CSS styles, HTML content, visual testing complete)

