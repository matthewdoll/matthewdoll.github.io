# Matthew Doll — personal site

Source for [matthewdoll.co.uk](https://matthewdoll.co.uk): a small personal site for scientific
computing side projects, CV, and contact details.

## What's here

A handful of small tools built on top of chemistry and computational work, each with the
code alongside a short write-up of what it does and why — rather than just a description
with no way to see how it works.

## Stack

Deliberately minimal: plain HTML, CSS and JavaScript, no framework, no build step. Hosted
on GitHub Pages.

Home page navigation is a Pt(NO)₃ diagram rather than a menu — clicking one of the three
atoms morphs it into the destination page via the native View Transitions API, no JS
router involved. Falls back to a plain instant page load in browsers that don't support
it yet (Firefox, at time of writing), and there's a conventional text nav in the header
regardless.

## Structure

- `index.html` — home, molecule nav
- `projects.html` — project index; a card + page per finished project
- `cv.html` — CV. Redacted for the web: no phone number or address in the page source,
  and excluded from search indexing
- `contact.html` — contact form (via Formspree, so no email address appears in the page
  source) plus a LinkedIn link
- `style.css` — shared styles
- `CNAME`, `robots.txt` — GitHub Pages / crawler config

## Adding a project

Each finished project gets a page under `projects/`, linked from a card in
`projects.html`. Template card markup is commented at the bottom of that file.
