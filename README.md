# MU Library Seat Management System: Lab 2 Accessible Check-in Interface

**Course:** ICT461 Advanced Web Technologies, Mulungushi University
**Lab:** Lab 2, Accessible Interface Design & Standards-Compliant Front-Ends
**Group:** Group O. Team lead for this lab: Joy Silishebo
**Author of this submission:** Dennis Sampa (202302571)
**Lecturer:** Kabaso B Winston (Mr.)

## What this is
A student seat check-in page for the MU Library Seat Management System, built with semantic HTML5, CSS and vanilla JavaScript. It targets WCAG 2.2 Level AA.

- Semantic landmarks: `header`, `nav`, `main`, `section`, `aside`, `footer`, plus a skip link
- 10-field form (text, tel, select, radio group, checkbox groups, textarea, consent), each with a native `<label for>`
- Colour contrast of at least 4.5:1 for text and 3:1 for UI components
- Visible 3 px focus rings, with keyboard order following the visual order
- Real-time validation with `aria-invalid`, `aria-describedby`, an `aria-live="polite"` status region and a `role="alert"` error summary

## Requirements
- A modern browser (Chrome, Edge or Firefox)
- Nothing else. There is no build step and no dependencies.
- Optional: Python 3 for a local server. Node.js 18+ only for the automated audit scripts.

## How to run
**Option 1:** open `site/checkin.html` by double-clicking it.

**Option 2:** serve it locally:
```
cd site
python -m http.server 8765
```
Then open http://localhost:8765/checkin.html (use `python3` on macOS/Linux).

## Folder layout
```
site/
  checkin.html   Page structure and form
  styles.css     Design system, contrast palette, focus styles
  app.js         Validation, ARIA updates, seat list, mock JSON payload
evidence/        Audit evidence used in the report
  lighthouse.report.html / .json
  axe_results.json
  tabstops.json  Keyboard focus path (17 stops)
  shot_*.png, fig_focus_*.png   Screenshots
tools/
  audit.js       axe-core + keyboard test (Playwright)
  shots.js       Screenshots of the audit reports
```

## Try it
1. Press **Check in** with the form empty to see the error summary and field errors.
2. Type 4 digits in Student ID and click away to see real-time validation.
3. Choose a floor to fill the Seat list (40 seats per floor).
4. Tab through the page to see focus rings. Shift+Tab goes back.
5. Submit a valid form to see the JSON payload.

## Validation rules
| Field | Rule |
|---|---|
| Student ID | Exactly 9 digits |
| Full name | 2 to 60 characters: letters, spaces, hyphens, apostrophes |
| Mobile number | Optional. `0971234567` or `+260971234567` |
| Programme, Floor, Seat, Planned stay | Required |
| Planned stay | 1 to 3 hours (3-hour maximum session) |
| Notes | Up to 200 characters |
| Location consent | Must be ticked |

## Audit results
- Lighthouse 13.5.0: Accessibility 100, Best Practices 100, SEO 100
- axe-core 4.14.0 (WCAG 2.0/2.1/2.2 A and AA, best practices): 0 violations in four page states (initial, after failed submit, after successful submit, 375 px mobile)
- Manual keyboard test: 17 tab stops, all with a visible focus ring

Re-run the Lighthouse step yourself in Chrome DevTools (Lighthouse tab), and the axe step with the axe DevTools extension.

## Known limitations
- The form displays a mock JSON payload and does **not** call the Flask `/api/checkin` endpoint yet.
- Client-side validation is for usability only. The server must repeat every check.
- Not yet tested with a screen reader (NVDA or VoiceOver).

## References
- W3C, Web Content Accessibility Guidelines (WCAG) 2.2: https://www.w3.org/TR/WCAG22/
- W3C, WAI-ARIA 1.2: https://www.w3.org/TR/wai-aria-1.2/
- WHATWG, HTML Living Standard: https://html.spec.whatwg.org/
- MDN Web Docs: https://developer.mozilla.org/
