# Spec Delta

## Purpose

Defines what the personal portfolio page presents about Fabrice: who he is, what he can do, what he has built, where he has worked and studied, and where to find him online.

## ADDED Requirements

### Requirement: Single-page structure
The site SHALL consist of one page that contains all content sections in this order: hero, about, skills, projects, experience and education. Each section other than the hero SHALL have a visible heading and an anchor so it can be linked directly.

#### Scenario: All sections on one page
- **WHEN** a visitor opens the site root
- **THEN** the hero, about, skills, projects and experience/education sections are all present on that single page, in that order

#### Scenario: Deep link to a section
- **WHEN** a visitor opens the site URL with a section anchor (e.g. `#projects`)
- **THEN** the browser scrolls to that section

### Requirement: Section navigation
The page SHALL provide a navigation element that links to the about, skills, projects and experience/education sections.

#### Scenario: Navigate to a section
- **WHEN** a visitor activates the "projects" navigation link
- **THEN** the page moves to the projects section

### Requirement: Hero introduction
The hero SHALL show Fabrice's full name as the page's main heading, his professional role, a short introduction of one to two sentences, and the profile links.

#### Scenario: First impression
- **WHEN** a visitor loads the page
- **THEN** the first visible content shows the name, role, introduction and profile links without scrolling on a typical desktop screen

### Requirement: About section
The page SHALL contain an about section with a short free-text description of who Fabrice is.

#### Scenario: About text present
- **WHEN** a visitor reaches the about section
- **THEN** it shows one or more paragraphs of descriptive text

### Requirement: Grouped skills
The page SHALL list skills grouped by category (for example backend, frontend, tools). Each group SHALL have a label and any number of skill items, and adding a skill or a group SHALL NOT require changes to styling.

#### Scenario: Skills shown by category
- **WHEN** a visitor reaches the skills section
- **THEN** each category label is shown together with its skills (e.g. "Backend" with Java, Spring Boot, C#)

#### Scenario: Adding a skill
- **WHEN** a new skill item is added to an existing group
- **THEN** it appears in that group with the same styling as the existing items

### Requirement: Project entries
The page SHALL list recent projects. Each project SHALL show a title, a short description and the technologies used, and MAY show links to its repository and/or a live version.

#### Scenario: Project with links
- **WHEN** a project has a repository URL and a live URL
- **THEN** its entry shows both links

#### Scenario: Project without links
- **WHEN** a project has no public repository or live version
- **THEN** its entry shows title, description and technologies, with no empty link placeholders

### Requirement: Experience and education timeline
The page SHALL list work experience and education as dated entries in reverse chronological order. Each entry SHALL show a period (start, end or "present"), a title (job title or degree) and an organisation (company or school), and MAY include a short description.

#### Scenario: Current position
- **WHEN** an entry is ongoing
- **THEN** its period ends with "present" (or an equivalent label) instead of an end date

#### Scenario: Experience and education distinguishable
- **WHEN** a visitor reads the timeline
- **THEN** they can tell work experience entries from education entries

### Requirement: Extensible profile links
The page SHALL link to Fabrice's GitHub and LinkedIn profiles. The list of profile links SHALL be extensible: adding a further link (e.g. GitLab or e-mail) SHALL take a single new entry and no changes to styling.

#### Scenario: Default links
- **WHEN** a visitor views the profile links
- **THEN** links to GitHub and LinkedIn are present, each with a visible or accessible label naming the platform

#### Scenario: Adding a GitLab link
- **WHEN** a GitLab entry is added to the profile links
- **THEN** it is displayed alongside the existing links with the same styling

### Requirement: External links open safely
Links to external sites (profiles, project repositories, live demos) SHALL open in a new tab and SHALL NOT give the opened page access to the opener.

#### Scenario: Opening a profile link
- **WHEN** a visitor activates the GitHub link
- **THEN** GitHub opens in a new tab and the portfolio page stays open

### Requirement: Page metadata
The page SHALL have a descriptive title, a meta description, a canonical URL of `https://fabrice-vj.ch/`, the language set to English, and the FvJ logo as favicon. The favicon SHALL have a fallback for browsers without SVG favicon support and a home-screen icon for iOS.

#### Scenario: Browser tab and search preview
- **WHEN** the page is shown in a browser tab or a search result
- **THEN** the tab shows the FvJ favicon and title, and the search snippet can use the meta description

#### Scenario: Saved to iOS home screen
- **WHEN** a visitor adds the page to an iPhone home screen
- **THEN** the shortcut uses the FvJ logo icon

### Requirement: Site logo in header
The header SHALL show the FvJ logo, linking back to the top of the page. The link SHALL have an accessible name, and the logo image SHALL NOT be announced separately.

#### Scenario: Logo returns to top
- **WHEN** a visitor activates the logo in the header
- **THEN** the page moves to the top

### Requirement: Link previews
The page SHALL provide Open Graph metadata (type, URL, title, description, image with dimensions and alt text) and a summary card type, so that sharing the URL shows a preview card. The preview description SHALL match the meta description. All preview URLs SHALL be absolute and point to `https://fabrice-vj.ch/`.

#### Scenario: Link shared on LinkedIn
- **WHEN** `https://fabrice-vj.ch` is pasted into a LinkedIn post or the LinkedIn Post Inspector
- **THEN** the preview shows the page title, the description and the FvJ logo image

#### Scenario: Link shared in a messenger
- **WHEN** the URL is shared in Slack, Teams or WhatsApp
- **THEN** a preview card with title, description and logo is shown instead of a bare link
### Requirement: Excluded content
The page SHALL NOT contain a blog, a profile photo, or a downloadable CV document.

#### Scenario: No downloadable CV
- **WHEN** a visitor looks through the page
- **THEN** there is no link to download a CV file (PDF or otherwise)
