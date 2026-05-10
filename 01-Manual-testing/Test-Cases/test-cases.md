# Test Cases – Wikipedia Search & Navigation

## Search Module (15 cases)

| ID              | Title                                                     | Priority/Type | Steps                                              | Expected Result                                                                                                                 |
| --------------- | --------------------------------------------------------- | -------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| WIKI-SEARCH-001 | Exact match redirects to canonical article                | Critical/Acceptance | Enter `Albert Einstein` → press Enter              | User is redirected to `/wiki/Albert_Einstein`; page title = “Albert Einstein”; no intermediate results page                     |
| WIKI-SEARCH-002 | Misspelled query triggers suggestion                      | High/Functional     | Enter `Einstien` → press Enter                     | Results page displayed; “Did you mean: Einstein” suggestion visible and clickable; clicking suggestion redirects correctly      |
| WIKI-SEARCH-003 | Ambiguous numeric query handled correctly                 | Medium/Functional   | Enter `2024` → press Enter                         | Either `/wiki/2024` OR a disambiguation page is shown; page content corresponds to the selected result; no error or blank state |
| WIKI-SEARCH-004 | Special character query returns correct technical article | High/Functional     | Enter `C++` → press Enter                          | Redirect to `/wiki/C%2B%2B`; page title contains “C++”; no encoding errors in URL                                               |
| WIKI-SEARCH-005 | Very long input handled without UI or server failure      | High/Destructive     | Paste ≥250 characters → press Enter                | Page loads within reasonable time (<3s); no crash, no layout break; either results or “no results” message shown                |
| WIKI-SEARCH-006 | Empty search submission handled gracefully                | High/Functional     | Leave field empty → press Enter                    | No navigation occurs OR user receives clear feedback; no error page or reload loop                                              |
| WIKI-SEARCH-007 | Whitespace-only input trimmed and handled                 | Medium/Functional   | Enter `"   "` → press Enter                        | Input treated as empty; behavior identical to empty search; no unexpected results                                               |
| WIKI-SEARCH-008 | Auto-suggest displays relevant results dynamically        | Medium/Functional   | Type `Ein` → wait 1–2s                             | Dropdown appears; suggestions include “Albert Einstein”; suggestions clickable and lead to correct page                         |
| WIKI-SEARCH-009 | “Go” action prioritizes exact match                       | High/Functional     | Enter `Python (programming language)` → click “Go” | Direct redirect to exact article; no intermediate search results                                                                |
| WIKI-SEARCH-010 | “Search” action returns ranked results list               | High/Functional     | Enter `Java` → click “Search”                      | Results page shown; most relevant/common article appears in top positions; list contains multiple distinct entries              |
| WIKI-SEARCH-011 | Search behavior consistent across pages                   | Medium/Functional   | Open any article → perform search                  | Same behavior as homepage (redirect vs results logic identical)                                                                 |
| WIKI-SEARCH-012 | Non-Latin query processed correctly                       | Medium/Compatibility   | Enter `αβγ` → press Enter                          | Relevant article (e.g., Greek alphabet) OR meaningful results page displayed; no encoding issues                                |
| WIKI-SEARCH-013 | Case-insensitive search works correctly                   | Medium/Functional   | Enter `aLbErT eInStEiN` → press Enter              | Redirect to canonical article; case does not affect result                                                                      |
| WIKI-SEARCH-014 | Diacritics handled correctly                              | Medium/Compatibility   | Enter `José` → press Enter                         | Results include relevant entries; diacritics do not prevent matching                                                            |
| WIKI-SEARCH-015 | Search available immediately after page load              | Medium/Performance   | Load homepage → immediately search                 | Input accepted without delay; no JS errors; result loads normally                                                               |


## Navigation Module (10 cases)

| ID           | Title                                           | Priority/Type | Steps                                      | Expected Result                                                                   |
| ------------ | ----------------------------------------------- | -------- | ------------------------------------------ | --------------------------------------------------------------------------------- |
| WIKI-NAV-001 | Sidebar “Contents” navigates correctly          | Medium   | Click “Contents”                           | Page scrolls to TOC anchor; URL updates with fragment (#)                         |
| WIKI-NAV-002 | “Random article” always loads valid page        | Medium   | Click “Random article”                     | A valid article page loads (title, content, URL `/wiki/...`); no error/blank page |
| WIKI-NAV-003 | Internal links navigate to correct destination  | High     | Click any inline link (e.g., “Physics”)    | Target article loads; title matches link context; no mismatch                     |
| WIKI-NAV-004 | Table of contents anchors scroll accurately     | High     | Click TOC section                          | Page scrolls to correct section; heading visible and aligned                      |
| WIKI-NAV-005 | Back-to-top restores initial viewport           | Medium   | Scroll down → click “Back to top”          | Smooth or instant scroll to top; no layout shift                                  |
| WIKI-NAV-006 | Category links display structured listings      | Medium   | Open category page                         | Subcategories and articles listed; links functional                               |
| WIKI-NAV-007 | Browser back/forward navigation preserves state | High/Functional     | Navigate across 3 pages → use Back/Forward | Pages reload correctly; no broken state or unexpected redirects                   |
| WIKI-NAV-008 | Links open correct URLs (no mismatch)           | High     | Hover + click multiple links               | Destination URL matches expected topic; no incorrect routing                      |
| WIKI-NAV-009 | No broken internal links (spot check)           | High/Functional     | Open 5+ links randomly                     | All return HTTP 200; no 404 pages                                                 |
| WIKI-NAV-010 | Deep navigation path remains stable             | Medium   | Navigate 5–6 links deep                    | No loss of functionality; consistent loading behavior                             |

## Usability & UI (8 cases)

| ID          | Title                                      | Priority/Type | Steps                        | Expected Result                                                       |
| ----------- | ------------------------------------------ | -------- | ---------------------------- | --------------------------------------------------------------------- |
| WIKI-UI-001 | Search bar visibility and accessibility    | High     | Open homepage + article page | Search bar visible without scrolling; interactive and not overlapped  |
| WIKI-UI-002 | Text readability meets usability standards | Medium   | View article (1920×1080)     | Font size (~16px+), spacing consistent; no visual strain              |
| WIKI-UI-003 | Color contrast meets WCAG AA               | High/Accessibility     | Inspect text/background      | Contrast ratio ≥ 4.5:1 for body text                                  |
| WIKI-UI-004 | Mobile layout responsive (320px)           | Critical | Emulate 320px width          | No horizontal scroll; elements fit viewport; menus usable             |
| WIKI-UI-005 | Images include meaningful alt attributes   | Medium   | Inspect images               | `alt` attribute present and descriptive (not empty unless decorative) |
| WIKI-UI-006 | No overlapping or clipped UI elements      | High/Compatibility     | Resize viewport (320–1024px) | Elements reposition correctly; no overlap                             |
| WIKI-UI-007 | Keyboard navigation works                  | High/Accessibility     | Navigate using Tab key       | Focus moves logically; interactive elements reachable                 |
| WIKI-UI-008 | Focus states are visible                   | Medium   | Tab through UI               | Visible outline or highlight on focused elements                      |

## Language Switching (6 cases)

| ID            | Title                                       | Priority/Type | Steps                           | Expected Result                                         |
| ------------- | ------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------- |
| WIKI-LANG-001 | Switching language loads equivalent article | High/Functional     | Switch EN → FR                  | French article loads; topic equivalent                  |
| WIKI-LANG-002 | Missing translation handled gracefully      | Medium   | Switch to unavailable language  | No broken page; either no link OR fallback behavior     |
| WIKI-LANG-003 | Interface language changes correctly        | Medium   | Change UI language              | Labels, menus translated consistently                   |
| WIKI-LANG-004 | Language list loads reliably                | Low      | Open language selector          | Loads within ~2 seconds; no UI freeze                   |
| WIKI-LANG-005 | URL updates correctly after switch          | High     | Switch language                 | URL reflects language domain (e.g., `fr.wikipedia.org`) |
| WIKI-LANG-006 | Search behavior consistent across languages | Medium   | Search same term in 2 languages | Results relevant per language; no errors                |
