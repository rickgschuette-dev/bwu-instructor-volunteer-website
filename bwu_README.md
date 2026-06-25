# Bridgewater Friends Forum — Volunteer Instructor & Facilitator Sign-Up

A single-file, self-contained HTML website hosting a volunteer recruitment form for the **Bridgewater Friends Forum**, the resident-led adult education program (a 55+ active adult HOA community in Brevard County, Florida).

Residents use the form to volunteer to teach or facilitate one of the program's classes. Submissions are collected through **Netlify Forms** — no backend code required.

## Key Technologies

- Plain HTML5 + CSS (no frameworks, no build step, no CDN dependencies)
- Inline JavaScript for client-side validation and AJAX submission
- [Netlify Forms](https://docs.netlify.com/forms/setup/) for serverless submission handling

## Files

- `BWU_InstructorVolunteer.html` — the canonical source file named per the project spec
- `index.html` — identical copy so the form is served at the site root (`/`)

The two files are kept in sync. If you edit one, copy it over the other.

## Form Details

- **Form name:** `bwu-instructor-volunteer`
- Spam protection via a hidden honeypot field (`bot-field`)
- All required fields use HTML5 `required` validation, plus a JS check that a class is chosen
- On success the form is hidden and an in-page thank-you confirmation is shown (AJAX, no page reload)

## Running Locally

It is a static file — open `index.html` directly in a browser to preview the layout. Note that **form submission only works once deployed to Netlify**, because submission processing is handled by Netlify's infrastructure.

To preview with Netlify's local emulation (including form handling):

```bash
netlify dev --port 8889
```

## Email Notifications

Netlify is configured to email new submissions. The notification recipient (**rick.g.schuette@gmail.com**) must be set once in the Netlify UI under **Project configuration → Notifications → Emails and webhooks → Form submission notifications**. This is an account-level setting and cannot be defined in the HTML.
