# Card Conjurer Enhanced — Copilot Instructions

## Project Overview

This is a fork of `joshbirnholz/cardconjurer` — a browser-based Magic: The Gathering proxy card generator.
The fork adds two major features: a **Preset System** and a **Project Manager** (batch/deck mode).
The app is built with vanilla JavaScript, HTML, and CSS, runs locally (no server required beyond static file serving), and targets export compatibility with MPCFill.

## Tech Stack

- **Language**: JavaScript (ES6+), HTML5, CSS3
- **Runtime**: Browser-based (no Node.js backend required for the app itself)
- **Build/Serve**: Python HTTP server, Docker, or WAMP/XAMPP for local development
- **External APIs**: Scryfall API (card data and images)
- **Canvas**: HTML5 Canvas API for card rendering
- **Storage**: localStorage + JSON file import/export

## Repository Setup

This project was forked from: https://github.com/joshbirnholz/cardconjurer
Owner's GitHub: DiegoPozzi1
The forked repository is located at: https://github.com/diegopozzi1/RLcardconjurer

## Coding Conventions

- Use camelCase for variables and functions
- Use PascalCase for class names and constructors
- Use UPPER_SNAKE_CASE for constants
- Prefer `const` over `let`; never use `var`
- Use ES6+ features: arrow functions, template literals, destructuring, async/await
- Keep functions focused and under 50 lines where possible
- Use JSDoc comments for all public functions
- Indent with 2 spaces
- Use single quotes for strings unless the string contains a single quote

## Architecture Principles

- Maintain backward compatibility with existing Card Conjurer functionality
- New features should be modular and self-contained in separate JS files
- Use the existing canvas rendering pipeline — do not replace it
- All new UI components should match the existing visual style unless a UI refactoring is explicitly approved
- Prefer progressive enhancement: existing users should not notice breaking changes

## File Organization

```text
cardconjurer/
├── index.html                    # Main app entry point
├── js/
│   ├── main.js                   # Existing core logic
│   ├── presets.js                # NEW: Preset system module
│   ├── projects.js               # NEW: Project manager module
│   ├── scryfall-batch.js         # NEW: Batch Scryfall API integration
│   └── export-mpcfill.js        # NEW: MPCFill-compatible export
├── css/
│   ├── style.css                 # Existing styles
│   └── features.css              # NEW: Styles for new features
├── data/
│   ├── presets/                   # NEW: Saved preset JSON files
│   └── projects/                  # NEW: Saved project JSON files
├── local_art/                    # User art assets (existing)
└── .github/
    ├── copilot-instructions.md   # This file
    ├── instructions/             # Path-specific instructions
    ├── prompts/                   # Reusable prompt files
    └── agents/                   # Custom agents


## Key Constraints

- The app must work entirely offline after initial setup (except Scryfall API calls)
- No build step required — vanilla JS only, no bundlers
- Must remain compatible with Docker deployment (port 4242)
- All saved data (presets, projects) must be exportable as JSON files
- Card images must export at up to 800 DPI for print quality
- Export naming must be MPCFill-compatible: `001_Card_Name.png`

## Error Handling

- Use try/catch for all async operations (especially Scryfall API calls)
- Provide user-friendly error messages in the UI
- Log errors to console with contextual information
- Implement graceful degradation when Scryfall is unreachable

## Testing Strategy

- Test locally using a Python HTTP server or Docker
- Verify card rendering output matches expected visual results
- Test preset save/load cycle integrity (save → close → reload → verify)
- Test project batch export produces correct file count and naming
- Test with various card types: creatures, planeswalkers, lands, artifacts, multicolor, tokens

## Workflow

- Branch naming: `feature/preset-system`, `feature/project-manager`, `refactor/ui` (if approved)
- Commit messages: imperative mood, descriptive (e.g., "Add preset color variant generation")
- PR descriptions should reference the feature specification
- All changes must be tested locally before committing