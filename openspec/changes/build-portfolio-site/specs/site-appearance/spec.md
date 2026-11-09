# Spec Delta

## Purpose

Defines how the portfolio page looks and adapts: a minimal dark theme that stays readable and usable on every screen size and for keyboard and assistive-technology users.

## ADDED Requirements

### Requirement: Dark minimal theme
The page SHALL always render with a dark background and light text, whatever the visitor's system colour-scheme preference. The design SHALL use one neutral palette and a single accent colour for interactive elements, with no decorative imagery.

#### Scenario: Visitor with light system theme
- **WHEN** a visitor whose operating system prefers a light colour scheme opens the page
- **THEN** the page still renders with the dark theme

#### Scenario: Interactive elements stand out
- **WHEN** a visitor looks at links and navigation items
- **THEN** they are shown in the accent colour or are otherwise clearly identifiable as interactive

### Requirement: Monospace typography
The page SHALL use the 0xProto monospace font and SHALL fall back to a system monospace font when 0xProto cannot be loaded, with the content still fully readable.

#### Scenario: Font service unavailable
- **WHEN** the web font fails to load
- **THEN** the text renders in a system monospace font and the layout remains intact

### Requirement: Readable contrast
Body text and link text SHALL meet WCAG 2.1 AA contrast (at least 4.5:1) against their background.

#### Scenario: Contrast check
- **WHEN** the page's text colours are checked with a contrast tool
- **THEN** every body and link text colour reaches at least 4.5:1 against its background

### Requirement: Responsive layout
The page SHALL be usable without horizontal scrolling at viewport widths from 320px upward. On narrow screens content SHALL stack in a single column. On wide screens the reading width SHALL be limited and projects MAY be shown in several columns.

#### Scenario: Phone width
- **WHEN** the page is viewed at 375px width
- **THEN** all sections are in a single column, project entries are stacked, and no content overflows horizontally

#### Scenario: Wide desktop
- **WHEN** the page is viewed at 1920px width
- **THEN** text lines stay at a comfortable reading length and projects are shown side by side

#### Scenario: Long content wraps
- **WHEN** a skill group or the profile links contain more items than fit on one line
- **THEN** the items wrap onto further lines instead of overflowing

### Requirement: Keyboard accessibility
All links and navigation items SHALL be reachable with the keyboard and SHALL show a clearly visible focus indicator.

#### Scenario: Tabbing through the page
- **WHEN** a visitor presses Tab repeatedly
- **THEN** focus moves through the navigation, profile links and project links in reading order, and the focused element is visibly highlighted

### Requirement: Semantic structure
The page SHALL use semantic landmarks (header/navigation, main, footer) and a logical heading hierarchy with exactly one top-level heading. Icon-only links SHALL have an accessible name.

#### Scenario: Screen reader navigation
- **WHEN** a screen-reader user lists the page's headings and landmarks
- **THEN** they find one top-level heading (the name), one heading per section, and navigation, main and footer landmarks

### Requirement: Respect reduced motion
Any transitions or smooth scrolling SHALL be disabled when the visitor's system requests reduced motion.

#### Scenario: Reduced motion preference
- **WHEN** a visitor with "prefers-reduced-motion: reduce" activates a navigation link
- **THEN** the page jumps to the section without animated scrolling

### Requirement: Works without JavaScript
All content and navigation SHALL be fully available with JavaScript disabled.

#### Scenario: JavaScript disabled
- **WHEN** the page is loaded with JavaScript disabled
- **THEN** all sections, links and navigation work exactly as with JavaScript enabled
