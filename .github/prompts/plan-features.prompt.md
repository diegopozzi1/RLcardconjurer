# Plan Feature Implementation

## Task

Create a detailed implementation plan for the two new features: Preset System and Project Manager.
Before implementing anything, analyze the existing codebase and produce a plan document.

## Context

The existing Card Conjurer app uses:
- A canvas-based rendering system in `js/` 
- Frame management with drag-and-drop layers
- Scryfall API integration for card data import
- JSON save/load for individual cards

## Feature 1: Preset System

### Requirements
- User creates a card manually (e.g., green creature with extended art border)
- User saves this configuration as a "preset" with a name
- System can auto-generate color variants (W, U, B, R, G, M, C, Land, Token) by swapping frame images
- Preset stores: frame style, set symbol (image + position), watermark (image + opacity + position), collector info template, border type, and any other repeatable settings
- When importing a card by name (via Scryfall), the system detects the card's color identity and applies the matching preset variant automatically
- Collector number auto-increments within a project context
- Presets are saved as JSON files and can be imported/exported

### Questions to investigate during planning
- How does the current frame system store frame references? (paths? URLs? base64?)
- What is the minimal set of data needed to reconstruct a card's "template" without the art?
- How does color identity map to frame selection in the current UI?
- Can we hook into the existing Scryfall import flow to auto-apply presets?

## Feature 2: Project Manager (Batch/Deck Mode)

### Requirements
- User creates a "project" (e.g., "My EDH Deck")
- User assigns a preset to the project
- User imports a card list (text format, one card per line, with optional quantity)
- System fetches all cards from Scryfall API (respecting rate limits: 50ms between requests)
- System applies the correct preset variant to each card based on color identity
- User navigates cards one by one (Prev/Next) to:
  - Upload or adjust custom art
  - Fine-tune text, flavor text color, or other per-card overrides
  - Mark card as "Done" or "Needs Review"
- Project saves progress as a JSON file (can be closed and reopened later)
- "Export All" downloads a ZIP file with all completed card images
- File naming follows MPCFill convention: `001_Card_Name.png`
- Project tracks: total cards, completed count, remaining count

### Questions to investigate during planning
- Does the current app support programmatic canvas rendering (render without UI interaction)?
- How to implement ZIP generation in-browser? (likely JSZip library)
- What's the best UX for the card navigation interface?
- How to handle Scryfall rate limiting for large lists (100+ cards)?

## UI Refactoring (OPTIONAL — Ask user first)

Before proceeding with UI changes, ASK ME:
> "The current Card Conjurer UI is functional but was designed for single-card editing. 
> The new features (especially Project Manager) may benefit from a UI restructuring 
> (e.g., tabbed interface, sidebar navigation, or a dedicated project view).
> Would you like me to:
> A) Keep the existing UI and add new features as additional panels/modals
> B) Propose a light UI refactoring to better accommodate the new features
> C) Propose a full UI redesign with a modern framework approach
> Please choose A, B, or C, or describe your preference."

## Output

Produce a `IMPLEMENTATION_PLAN.md` file in the project root with:
1. Codebase analysis summary (key files, architecture, extension points)
2. Feature 1 detailed plan (modules, data structures, UI changes, integration points)
3. Feature 2 detailed plan (modules, data structures, UI changes, integration points)
4. Dependency list (any external libraries needed, e.g., JSZip)
5. Implementation order and phases
6. Risk assessment and mitigation strategies
7. Estimated complexity per module (Small/Medium/Large)