# Kim and Ben: Lab 2 Website

**Live site:** https://jessesimam-sys.github.io/team-website/

## Team
| Name | Registration no. | GitHub username |
|------|------------------|-----------------|
| Jesse Kimutai | COM/8353/26 | jessesimam-sys |
| Benedict Mochabo | COM/3493/26 | Bene-cmyk |

## Who drove each part
- Part 0, 2, 4: Jesse Kimutai (Partner A)
- Part 1, 3: Benedict Mochabo (Partner B)

## Personalisation
- Our colours: blue theme. Contrast ratios were checked against the WCAG 4.5 : 1 minimum.
  - Light mode: `--color-primary: #1d4ed8` (6.70 : 1 on white, 6.23 : 1 on the page background), `--color-primary-dark: #1e3a8a` (10.36 : 1 on white), white text on primary (6.70 : 1).
  - Dark mode: `--color-primary: #7db0ff` (7.35 : 1 on the dark surface, 8.24 : 1 on the dark background), `--color-primary-dark: #b5d2ff` (10.51 : 1 on the dark surface), `--color-on-primary: #0a1630` on primary (8.14 : 1).
- Projects we added: Co-authored Git workflow (Git), GitHub Pages deployment (Git), Searchable project list (JavaScript), FAQ page (HTML). Git is a new category, with its own entry in `categoryNames` and its own filter button.
- Extension challenge(s) completed: E1 (fourth page, `faq.html`, using `<details>` and `<summary>`), E2 (follows the system theme when nothing is saved), E3 (project search combined with the active filter), E4 (contact form draft saved to `localStorage`).

## Reflection
1. A `<div>` would not be reachable with the `Tab` key and would not respond to `Enter` or `Space`, and screen readers would not announce it as a button or report whether the menu is expanded. Keyboard-only users, screen-reader users and people using switch devices would be affected. A real `<button>` gives all of this for free, while a `<div>` needs extra attributes and scripting to imitate it.
2. Without `defer`, the browser stops parsing the HTML when it reaches the script in the `<head>` and runs it immediately, before `<body>` exists. Then `document.body` and every element we select would be missing, so the theme code would throw an error and the other features would silently do nothing. `defer` makes the script run only after the HTML is fully parsed.
3. `innerHTML` treats text as HTML, so a visitor could type something like `<script>` or an `<img onerror=...>` tag as a project title and the browser would run it for everyone who views the page. This is cross-site scripting, and it could steal data or change the page. `textContent` always shows the text as plain characters, so nothing is executed.
4. Browser validation can be bypassed by turning off JavaScript, editing the page in DevTools or sending a request directly with a tool like `curl`. It only helps honest users fix mistakes quickly. The server must check everything again because it cannot trust anything that comes from the client.
5. An origin is the combination of protocol, host and port, and `localStorage` is kept separately for each origin. Home and Contact both load from `http://127.0.0.1:5500`, so they share the saved theme. A double-clicked file uses `file://`, which is a different origin with its own separate storage.
6. The header, navigation and footer are copied into every HTML page. Changing the team name or adding a link, as we did when adding the FAQ page, means editing every file, and missing one leaves the site inconsistent. This can be avoided with reusable components in a framework such as React, with a static site generator or templates, or by having JavaScript insert the shared parts.
