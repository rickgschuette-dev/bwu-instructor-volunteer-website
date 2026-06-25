# AGENTS.md

## Project Overview

Static single-page volunteer recruitment form for the **Bridgewater Friends Forum** (a resident-led adult-education program). Built as plain HTML/CSS/JS with no framework or build pipeline. Submissions flow through Netlify Forms.

## Architecture

- **`BWU_InstructorVolunteer.html`** — the source of truth. The filename is mandated by the project spec; do not rename it.
- **`index.html`** — a byte-for-byte copy of the above, present only so the form is served at the site root. Keep both in sync: after editing `BWU_InstructorVolunteer.html`, run `cp BWU_InstructorVolunteer.html index.html`.

Everything (markup, CSS in a `<style>` block, JS in a `<script>` block) lives inline in a single file. There is intentionally no external CSS/JS, no CDN, and no dependencies.

## Netlify Forms

- Form `name` attribute and the hidden `form-name` input must both equal `bwu-instructor-volunteer`.
- The form is submitted via AJAX (`fetch('/')` with `Content-Type: application/x-www-form-urlencoded`) so the confirmation can render in place. Because this is a static HTML file (not an SPA), Netlify's build bot still detects the form at deploy time and POSTs to `/` are processed correctly.
- Spam protection: `data-netlify-honeypot="bot-field"` plus a hidden `bot-field` input.
- **After any change touching the form, the Netlify Forms feature must be enabled for the deploy** by running:
  ```bash
  node /opt/buildhome/.claude/skills/netlify-forms/scripts/enable.cjs
  ```

## Design Tokens (CSS custom properties in `:root`)

Match the Bridgewater Friends Forum brand:
- Navy `#1a3a5c`, Gold `#c8922a` (hover `#b07a1e`), Background `#f9f7f4`, Card cream `#fdf8f1`
- Border/divider `#d4c9b0`, Success green `#2a7a4b`, Light blue-gray `#cde0f5`
- Body font: Georgia serif, 17px, line-height 1.7. Labels/headings: Arial bold navy.

## Conventions

- Keep the file dependency-free and self-contained.
- Preserve the exact field names, order, and the dropdown's `<optgroup>` grouping — these match downstream expectations for submission data.
- Do not run build commands; Netlify validates the deploy automatically.

## Non-Obvious Decisions

- Two identical HTML files exist on purpose (spec-mandated filename vs. servable root). This is not redundant cruft.
- Email notification recipient (`rick.g.schuette@gmail.com`) is configured in the Netlify UI, not in code.
