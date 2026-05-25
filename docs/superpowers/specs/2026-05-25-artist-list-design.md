# Artist List Implementation - Festival Program Page

**Date:** 2026-05-25
**Component:** Festival Program Page
**Objective:** Add artist lineup to the program page with custom typography

## Overview

Replace the "Stay tuned" placeholder on the festival program page with a complete list of 23 performing artists. Use the custom Untitled1-Regular font for artist names to create visual distinction while maintaining the site's minimalist aesthetic.

## Requirements

### Content
- Display 23 artist names in alphabetical order
- Bilingual section title: "Artisti & Performers" (IT) / "Artists & Performers" (EN)
- Artist names remain the same in both languages (proper nouns)

### Artist List (Alphabetical)
1. Alice Flaviana
2. Amphibia
3. Bassi Gradassi
4. Chantssss
5. Classical Hooligans
6. Carl Ahnebrink (FLEE Project) + Alan Bolumarrli
7. Enrico Malatesta
8. Flux by Uchina
9. Giesse
10. Habitat T.P.U.
11. Jungla
12. Lorenzo Travaglini
13. La Messinscena
14. Lemethi
15. Proxy Bar
16. Mira
17. Nicolas Gaunin
18. Oleno e Matte
19. Privato
20. Ramzi
21. Reptilian Expo
22. Señor Service
23. Sister Effect
24. Yulia Kachan

### Design Specifications

**Layout:**
- Vertical centered list
- One artist name per line
- Consistent with existing page alignment

**Typography:**
- Font: Untitled1-Regular (custom font from Archivio folder)
- Size: 0.95rem for artist names
- Line height: 1.8 for comfortable spacing
- Color: #333 (matching existing prose text)
- Fallback: 'Courier New', Courier, monospace

**Visual Separation:**
- Horizontal rule (`<hr>`) before the artist section
- Section title styled like existing `<h1>` (uppercase, letter-spacing, bottom border)

**Bilingual Integration:**
- Title uses existing `data-it` / `data-en` pattern
- Automatically switches with language toggle (no JS changes needed)

## Architecture

### Approach: Self-Contained Inline Implementation

All changes contained within the program page to maintain independence from other festival pages.

**File Structure:**
```
formulario-frontend/festival/program/
├── index.html          (modified)
└── fonts/              (new)
    ├── Untitled1-Regular.woff2
    ├── Untitled1-Regular.woff
    └── Untitled1-Regular.otf
```

**Why this approach:**
- Page already uses inline CSS (coherent with existing pattern)
- Zero risk of impacting other festival pages
- Complete autonomy - all resources local to program/
- Simplifies deployment

### Font Loading Strategy

Use `@font-face` with three format variants for browser compatibility:
- `.woff2` - modern browsers (smallest file, loads fastest)
- `.woff` - older browser support
- `.otf` - ultimate fallback

`font-display: swap` ensures text is visible immediately while custom font loads.

## HTML Structure

Replace existing `.prose` div (lines 240-248) with:

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

**Rationale:**
- Semantic `<h2>` for accessibility
- Individual `<div>` per artist for precise styling control
- Consistent with bilingual pattern (data-it/data-en attributes)

## CSS Implementation

Add to existing `<style>` tag (after line 145, before closing `</style>`):

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

**Design Decisions:**
- Title mirrors `<h1>` style (uppercase, letterspacing, border-bottom) for visual consistency
- Artists list centered to match existing page alignment
- Font stack includes fallbacks for graceful degradation
- `line-height: 1.8` provides comfortable reading spacing without overwhelming the list

## Integration Points

### Bilingual System
Existing JavaScript (lines 258-268) already handles language switching for all elements with `data-it` and `data-en` attributes. The new `<h2>` follows this convention and requires no JS modifications.

**No changes needed to:**
- Language toggle buttons
- JavaScript event handlers
- Translation logic

### Existing Styles
New CSS classes (`.artists-title`, `.artists-list`, `.artist-name`) do not conflict with existing styles. They are scoped specifically to the artist section.

### Navigation & Links
Artist names are static text (no links, no interactions). This decision keeps the page simple and fast, consistent with the current "stay tuned" approach.

## Implementation Checklist

1. **Create font directory:**
   - Create `formulario-frontend/festival/program/fonts/`

2. **Copy font files:**
   - Copy `Untitled1-Regular.woff2` from `/Users/marco/Desktop/Archivio/`
   - Copy `Untitled1-Regular.woff` from `/Users/marco/Desktop/Archivio/`
   - Copy `Untitled1-Regular.otf` from `/Users/marco/Desktop/Archivio/`

3. **Update HTML:**
   - Remove lines 240-248 (`.prose` div with "Stay tuned")
   - Add `<hr>` separator
   - Add `<h2>` with bilingual title
   - Add `.artists-list` div with all 24 artist names

4. **Update CSS:**
   - Add `@font-face` declaration
   - Add `.artists-title` styles
   - Add `.artists-list` styles
   - Add `.artist-name` styles

5. **Test:**
   - Verify font loads correctly
   - Test language toggle (IT/EN) switches title
   - Check responsive behavior on mobile
   - Confirm visual alignment with rest of page

## Success Criteria

- [ ] All 24 artist names visible in alphabetical order
- [ ] Untitled1-Regular font applied to artist names
- [ ] Title switches between IT and EN when language toggled
- [ ] Visual consistency with existing page design
- [ ] Font loads with appropriate fallbacks
- [ ] Page remains performant (font files optimized)
- [ ] Mobile responsive (list readable on small screens)

## Notes

- Font files total ~450KB (reasonable for web use)
- Browser support: all modern browsers + IE11 (via .woff fallback)
- No accessibility concerns: semantic HTML, sufficient contrast, readable font size
- No breaking changes: only additive modifications to the page
