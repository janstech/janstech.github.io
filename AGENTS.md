````markdown
# AGENTS.md

## Purpose

This repository contains the personal software-development portfolio of Jan Sarivuo.

The live site is published with GitHub Pages and presents:

- Jan Sarivuo as a software developer
- published Android applications
- full-stack and backend projects
- infrastructure and DevOps experience
- architecture documentation
- AI-assisted software-development experience
- the JanstechApps application brand

The primary audiences are:

- employers and recruiters
- potential clients
- technical collaborators
- application users interested in the developer behind JanstechApps

The site must remain credible, professional, technically accurate, accessible, responsive, and easy to maintain.

---

## Repository

Local repository:

```text
C:\Dev\personal_portfolio
````

Remote repository:

```text
git@github.com:janstech/janstech.github.io.git
```

Production site:

```text
https://janstech.github.io/
```

Application brand site:

```text
https://janstechapps.com/
```

The portfolio and JanstechApps serve different but complementary purposes:

* `janstech.github.io` presents Jan Sarivuo as a developer and documents his technical work.
* `janstechapps.com` presents the applications and the JanstechApps product brand.

Do not turn the personal portfolio into a generic company landing page.

---

## Technology and architecture

The portfolio is intentionally implemented as a lightweight static site.

Primary technologies:

* HTML
* CSS
* vanilla JavaScript
* GitHub Pages

Do not introduce a framework, package manager, bundler, CSS framework, component library, or build system without explicit approval.

In particular, do not migrate the site to:

* React
* Next.js
* Astro
* Vue
* Svelte
* Tailwind CSS
* Bootstrap
* a static-site generator

A framework migration is not a visual redesign requirement.

Prefer improvements that fit the existing static architecture.

---

## Important files and directories

Inspect the repository before making changes. Important locations may include:

```text
index.html
apps/index.html
gainsai/index.html
css/
images/
assets/
documents/
docs/
README.md
sitemap.xml
robots.txt
manifest.json
```

Do not assume that every page uses exactly the same local CSS or JavaScript structure. Audit the relevant files before editing.

When adding a new project page, use the closest existing project page as the structural reference.

---

## Working method

Before modifying code:

1. Read this file.
2. Check `git status`.
3. Inspect the relevant HTML, CSS, JavaScript, documentation, and recent Git history.
4. Understand the existing implementation before proposing a replacement.
5. Identify whether the task is an audit, implementation, correction, or validation task.
6. Preserve unrelated work already present in the working tree.

Do not overwrite, revert, discard, or reformat unrelated changes.

If the working tree is not clean, determine which changes belong to the current task before editing.

Prefer focused, reviewable changes over large rewrites.

---

## Claude Code and Codex collaboration

This repository is worked on alternately with Claude Code, Codex, and manual edits.

All agents must:

* treat the repository state as the source of truth
* inspect recent commits and current diffs before working
* avoid reimplementing work that another agent has already completed
* preserve established conventions unless a change is explicitly justified
* document significant architectural or visual decisions
* leave the repository in a state that another agent can understand and continue from

Do not add agent-specific instructions that conflict with this file.

Do not create separate competing implementations for Claude Code and Codex.

When continuing earlier work, inspect:

```powershell
git status
git log --oneline -10
git diff
```

Use additional Git inspection when needed.

---

## Language support

The site is bilingual:

* Finnish
* English

The existing FI/EN language-switching mechanism must be preserved.

The current implementation uses translation keys such as:

```html
data-i18n="..."
```

and JavaScript translation dictionaries.

Some elements may also use attributes such as:

```html
data-i18n-alt="..."
data-i18n-aria="..."
```

Use the existing mechanism. Do not create a parallel translation system.

All new user-visible content must be provided in both Finnish and English, including when applicable:

* headings
* paragraphs
* project descriptions
* navigation labels
* buttons
* links
* status labels
* captions
* image alternative text
* ARIA labels
* page titles
* interface messages

Translations must be natural in each language. Do not use mechanical word-for-word translation.

When editing translations:

* keep FI and EN keys in parity
* check for missing keys
* check for unused keys
* verify that the active language persists according to the existing implementation
* update `<html lang>` when required by the existing language logic
* make sure longer Finnish text does not break the layout

Do not hard-code visible text that remains in the wrong language after switching languages.

---

## Content accuracy

All portfolio claims must be truthful and supportable.

Do not invent:

* user counts
* download counts
* ratings
* reviews
* revenue
* conversion rates
* customer testimonials
* performance improvements
* usage statistics
* employers
* clients
* certifications
* project outcomes
* features not present in the source project

Do not exaggerate prototype work as production work.

Published applications may be described as production applications only when that status is verified.

When information is uncertain, inspect the relevant project repository or documentation before writing it.

Potential project source repositories exist outside this repository. They may be inspected as read-only sources when explicitly relevant, but they must not be modified during portfolio work.

For example, GainsAI information may be checked from:

```text
C:\Dev\GainsAI\codex\gains-ai
```

Never copy secrets or internal operational details from another repository into the portfolio.

---

## Sensitive information

Never publish:

* API keys
* passwords
* tokens
* private keys
* service-account files
* database credentials
* `.env` contents
* purchase tokens
* authentication tokens
* internal user data
* private logs
* personal test-account information
* server IP addresses unless explicitly approved
* internal administrative URLs
* unnecessary infrastructure commands
* confidential business information

Do not expose private development or production diagnostics merely to make a project description look technical.

Public portfolio content should explain architecture and engineering capability without exposing operational secrets.

---

## Portfolio positioning

The portfolio should communicate that Jan can deliver complete software products.

Important capabilities include:

* Android development with Kotlin and Jetpack Compose
* full-stack development
* FastAPI and Python backends
* MariaDB and MySQL
* REST APIs and integrations
* Firebase Authentication and App Check
* Google Play Integrity
* Google Play Billing
* Linux and Hetzner production environments
* Nginx, Apache, systemd, deployments, logs, and troubleshooting
* encrypted backups and restore testing
* architecture documentation
* AI-assisted software development
* independently published applications

The portfolio must distinguish between:

1. technologies Jan has used
2. systems Jan has built
3. production responsibilities Jan has handled
4. applications Jan has published

Avoid presenting the skills section as only a generic keyword list.

---

## JanstechApps

JanstechApps is Jan's independent application brand.

The portfolio may link to and explain JanstechApps, but the treatment must remain proportionate.

Suitable framing:

* JanstechApps is the home of Jan's published applications.
* Jan designs, develops, publishes, and maintains applications under the brand.
* The personal portfolio focuses on Jan's skills, projects, engineering decisions, and professional profile.
* JanstechApps focuses on applications and product presentation.

Avoid making the portfolio look like an advertisement or a corporate marketing site.

Use the exact brand spelling:

```text
JanstechApps
```

Use the exact domain:

```text
janstechapps.com
```

---

## Visual design principles

The visual direction should be:

* professional
* distinctive
* calm
* modern
* polished
* technically credible
* readable
* appropriate for a Finnish software developer
* attractive without looking overdesigned

The site should feel intentionally designed by a human.

Avoid the stereotypical AI-generated portfolio aesthetic.

Do not default to:

* excessive blue-purple gradients
* glowing borders on every element
* glassmorphism everywhere
* floating abstract blobs
* decorative particle backgrounds
* oversized empty hero sections
* excessive rounded cards
* many nested card surfaces
* generic technology badge walls
* unnecessary animated counters
* fake terminal animations
* constant movement
* meaningless visual decoration
* generic slogans about “building the future”
* a design that resembles an off-the-shelf portfolio template

Dark styling is acceptable, but it must not become a monotonous collection of nearly identical dark cards.

Use contrast, spacing, typography, imagery, and hierarchy deliberately.

---

## Design consistency

Use shared visual rules wherever practical:

* color tokens
* typography scale
* spacing scale
* content widths
* border radii
* borders
* shadows
* button styles
* links
* focus states
* card treatments
* image treatments

Do not introduce arbitrary one-off values throughout the code.

Prefer CSS custom properties for reusable design values.

Do not perform a full design-system rewrite unless the task explicitly requires it.

When changing shared CSS, verify every page affected by that stylesheet.

---

## Typography

Typography must prioritize readability and visual hierarchy.

Check:

* heading hierarchy
* line length
* line height
* font weight
* paragraph spacing
* list readability
* mobile wrapping
* Finnish compound words
* English and Finnish content differences

Avoid extremely large headings that push meaningful content below the fold.

Avoid long full-width paragraphs.

Do not rely on very light text contrast for secondary content.

External fonts should only be introduced after considering:

* loading performance
* privacy
* fallback behavior
* visual benefit
* licensing and delivery method

---

## Hero section

The hero must quickly explain:

* who Jan is
* what kind of developer he is
* what he has built
* what the visitor should explore next

It must not resemble a generic startup landing page.

Avoid vague claims and empty slogans.

The existing code-themed presentation may be retained, refined, or replaced only after evaluating whether it supports the overall hierarchy and authenticity.

The hero should not overemphasize “junior” at the expense of demonstrated production experience, but it must remain factually accurate.

---

## Projects

Projects are the portfolio's strongest evidence.

Prioritize projects based on professional relevance and current status.

Published Android applications and complete end-to-end systems should generally receive more prominence than old learning projects.

Important applications may include:

* GainsAI
* Kauppalista & Muistiinpanot
* WaveIQ
* SureKeep
* Työtori

Do not assume every application must have equal visual weight.

When restructuring the projects section, consider clear groups such as:

* published applications
* full-stack and integration projects
* infrastructure and operations
* earlier or experimental projects

Do not remove a project without explicit approval.

Large project descriptions on the home page may be condensed, with deeper technical information moved to project-specific pages.

Every project link must remain functional.

For external links opened in a new tab, use appropriate security attributes:

```html
target="_blank" rel="noopener noreferrer"
```

---

## Application screenshots

Application screenshots must:

* retain their correct aspect ratio
* remain readable
* load efficiently
* work on mobile
* include meaningful localized alternative text when required
* avoid unnecessary cropping
* avoid distortion
* follow a consistent visual treatment

Do not replace authentic screenshots with invented interfaces.

Do not add device mockups merely because they are fashionable. Use them only when they improve presentation without hiding the real UI.

Prefer explicit `width` and `height` attributes where practical to reduce layout shifts.

Use lazy loading for below-the-fold imagery when appropriate.

Do not commit unnecessarily duplicated large source images without evaluating their purpose.

---

## Accessibility

Accessibility is a required part of the implementation.

Maintain or improve:

* semantic HTML
* one logical primary `<h1>` per page
* heading hierarchy
* keyboard navigation
* visible focus states
* meaningful link text
* button semantics
* image alternative text
* ARIA labels where genuinely needed
* sufficient color contrast
* language attributes
* reduced-motion behavior
* touch-target sizes
* responsive text wrapping

Do not use ARIA to compensate for incorrect native HTML semantics.

Do not convey state or meaning through color alone.

Language buttons should expose their active state accessibly, for example with `aria-pressed` when consistent with the current implementation.

---

## Responsive design

All visible changes must be checked at representative widths:

* 360 px
* 390 px
* 768 px
* 1024 px
* 1440 px

Verify both Finnish and English where text length may affect layout.

Check at minimum:

* header and navigation
* language switch
* hero
* buttons
* skills
* project grids
* project images
* long headings
* lists
* footer
* project-specific pages

The site must not produce unintended horizontal scrolling.

Do not solve responsive problems with brittle device-specific hacks when a flexible layout can solve them.

---

## Motion and interaction

Motion must be restrained and purposeful.

Acceptable uses may include:

* subtle hover feedback
* short entrance transitions
* clear menu transitions
* small state changes

Avoid:

* constant background movement
* distracting parallax
* animated text that delays reading
* excessive scroll-triggered effects
* motion required to understand content

Respect:

```css
@media (prefers-reduced-motion: reduce)
```

The site must remain fully usable without animation.

---

## Performance

The site should remain fast and lightweight.

Avoid:

* large JavaScript libraries
* unnecessary third-party scripts
* autoplay media
* oversized images
* duplicate image assets
* blocking resources
* excessive font files
* unnecessary animations
* loading an entire icon library for a few icons

Where practical:

* specify image dimensions
* lazy-load below-the-fold images
* use suitable image formats
* minimize layout shifts
* keep JavaScript small
* avoid render-blocking additions

Do not optimize by reducing image quality to an obviously poor level.

---

## SEO and social metadata

Preserve and improve, where relevant:

* `<title>`
* meta description
* canonical URL
* robots directives
* Open Graph metadata
* Twitter/X card metadata
* sitemap entries
* valid internal links

Canonical and Open Graph URLs should use production absolute URLs.

Do not add duplicate metadata.

Do not claim language-specific metadata support that the current architecture does not actually implement.

When adding a new public page:

* use the existing URL structure
* add it to `sitemap.xml` when appropriate
* ensure canonical URL correctness
* provide a suitable social image when available
* verify that links and image URLs work on GitHub Pages

---

## Code quality

Keep HTML, CSS, and JavaScript understandable and maintainable.

Prefer:

* semantic class names
* shared styles
* small focused functions
* consistent formatting
* comments only where they add real value
* progressive enhancement
* robust relative and absolute paths

Avoid:

* excessive inline styles
* duplicated large CSS blocks
* global selectors with unintended effects
* unexplained magic numbers
* large unstructured scripts
* fragile DOM assumptions
* unnecessary abstractions for a small static site

Do not reformat entire files when only a small functional change is required.

Preserve the repository's existing line-ending conventions unless a dedicated normalization task has been approved.

---

## Line endings and diffs

Some existing files may use CRLF line endings.

Do not normalize an entire file from CRLF to LF or vice versa as a side effect of a small edit.

Before finalizing:

```powershell
git diff --stat
git diff
git diff --check
```

If `git diff --check` reports issues caused by known pre-existing line-ending behavior, investigate and report the exact cause.

Do not automatically create a massive unrelated line-ending diff to silence the check.

Ensure that no actual trailing whitespace or accidental tab changes were introduced.

---

## Validation

Perform validation appropriate to the scope of the task.

For visible page changes, check:

* pages load successfully
* internal links work
* external links are correct
* images load
* image aspect ratios are preserved
* no new console errors appear
* no unintended horizontal overflow exists
* language switching works
* FI and EN translations are complete
* active language persists
* mobile and desktop layouts work
* keyboard navigation works
* focus states remain visible
* headings are logical
* HTML is structurally sound

If a local static server is needed, use an available lightweight method.

Example:

```powershell
python -m http.server 8000
```

Use Playwright or another existing browser-testing setup when available.

Do not add a permanent testing dependency solely for a one-time manual inspection unless approved.

When relevant, also check:

* sitemap parsing
* duplicate URLs
* canonical URLs
* Open Graph image paths
* missing translation keys
* orphaned translation keys
* broken local resource paths
* secrets in newly added lines

---

## Documentation

Document substantial visual, architectural, or content-structure decisions under `docs/` when useful.

Examples include:

* redesign audit
* design direction
* implementation plan
* architecture change
* content restructuring rationale

Do not create documentation for trivial copy changes.

Documentation should explain:

* the problem
* the chosen solution
* important constraints
* alternatives considered
* validation performed

Do not generate long documentation that merely repeats the source code.

---

## Git and commits

Do not push unless Jan explicitly requests it.

Do not force-push.

Do not rewrite published history.

Do not amend an existing commit unless explicitly requested.

Do not create a commit unless the task requests a commit or Jan approves it.

When a commit is requested:

* inspect the final diff
* include only files belonging to the task
* use a concise English commit message
* report the commit hash
* report whether the branch is ahead of the remote
* do not push automatically

Example commit style:

```text
Refine portfolio project presentation
Add JanstechApps brand introduction
Improve bilingual portfolio metadata
Redesign portfolio visual hierarchy
```

Avoid vague messages such as:

```text
Update files
Changes
Fix stuff
```

---

## Prohibited actions without explicit approval

Do not:

* push to GitHub
* deploy manually
* force-push
* delete project content
* remove existing public URLs
* migrate to a framework
* replace the translation architecture
* redesign the whole site during an audit-only task
* add analytics or tracking services
* add advertising
* add cookie banners without an actual need
* publish secrets or private operational details
* invent claims or statistics
* modify unrelated repositories
* replace authentic screenshots with generated interfaces
* rewrite the entire site in one uncontrolled change
* discard manual changes
* reset the working tree
* run destructive Git commands

Potentially destructive commands such as the following require explicit approval:

```text
git reset --hard
git clean -fd
git checkout -- .
git restore .
git rebase
git push --force
```

---

## Audit-only tasks

When instructed to audit or plan:

* inspect the current implementation
* identify strengths and weaknesses
* produce recommendations
* create documentation only when requested
* do not start the full implementation
* do not modify visible production content
* do not commit unless requested
* do not push

Clearly separate:

1. observations
2. recommendations
3. proposed implementation
4. changes actually made

Do not describe proposed work as completed work.

---

## Redesign tasks

For a visual redesign:

1. Audit the current site.
2. Preserve the strongest existing content.
3. Establish the visual direction.
4. Define shared design tokens.
5. Implement in reviewable phases.
6. Validate each phase.
7. Avoid a single high-risk rewrite.

Suggested implementation boundaries:

1. visual foundations and tokens
2. header and hero
3. skills and professional positioning
4. project hierarchy and cards
5. project-detail pages
6. JanstechApps integration
7. responsive and accessibility polish
8. performance and SEO validation

Each phase should be independently reviewable and revertible.

---

## Final report

At the end of a task, report clearly:

* what was inspected
* what was changed
* files added or modified
* important implementation decisions
* translations added or changed
* validation performed
* validation limitations
* unresolved questions
* `git status`
* commit hash, when a commit was created
* whether anything was pushed

Do not claim a validation passed unless it was actually executed.

Do not hide failures. Explain their impact and likely cause.

---

## Core principle

The portfolio should demonstrate real engineering work through clear content, authentic applications, thoughtful design, and verifiable technical depth.

Every change should strengthen at least one of these:

* clarity
* credibility
* visual hierarchy
* usability
* accessibility
* maintainability
* performance
* accurate representation of Jan's work

Avoid changes that add visual novelty without improving the portfolio.

```