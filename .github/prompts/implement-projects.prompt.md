# Implement Project Manager

## Prerequisites

- [ ] Preset System is implemented and working
- [ ] `IMPLEMENTATION_PLAN.md` has been reviewed and approved
- [ ] Feature branch `feature/project-manager` is active

## Task

Implement the Project Manager (Batch/Deck Mode) as described in the implementation plan.

## Implementation Steps

1. **Create `js/projects.js` module**
   - Define Project data structure (JSON schema)
   - Implement `createProject(name, presetPack)` — initializes a new project
   - Implement `importCardList(textList)` — parses card names, handles quantities
   - Implement `fetchAllCards(cardNames)` — batch Scryfall fetch with rate limiting
   - Implement `applyPresetsToAll(project)` — applies preset variants to all cards
   - Implement `navigateCard(project, direction)` — prev/next navigation
   - Implement `updateCardStatus(project, cardIndex, status)` — mark done/review
   - Implement `saveProject(project)` / `loadProject(jsonFile)` — persistence
   - Implement `exportAllCards(project)` — batch render and ZIP download

2. **Create `js/scryfall-batch.js` module**
   - Implement rate-limited batch fetching (50ms delay between requests)
   - Handle errors gracefully (card not found, network issues)
   - Cache responses to avoid re-fetching
   - Support the Scryfall `/collection` endpoint for bulk lookups

3. **Create `js/export-mpcfill.js` module**
   - Implement batch canvas rendering (programmatic, no UI interaction needed)
   - Generate ZIP file using JSZip
   - Name files following MPCFill convention: `{number}_{Name_With_Underscores}.png`
   - Support configurable DPI/resolution
   - Show progress indicator during export

4. **Create Project UI**
   - "Projects" tab/section in the interface
   - "New Project" dialog (name + preset selection)
   - Card list import textarea (paste decklist)
   - Card navigation bar: [← Prev] [Card 3/100] [Next →]
   - Per-card status indicators (Done ✅ / Review ⚠️ / Pending ⏳)
   - Art upload/adjustment area for current card
   - Per-card override panel (flavor text color, custom text, etc.)
   - Progress summary bar (47/100 completed)
   - "Export All" button with progress indicator
   - "Save Project" / "Load Project" buttons

5. **Integrate with Preset System**
   - When creating a project, user selects a preset pack
   - Each card in the list gets the appropriate color variant applied
   - Per-card overrides are stored separately from the preset

6. **Persistence**
   - Save projects to localStorage (with size warnings for large projects)
   - Provide JSON export/import for project files
   - Store in `data/projects/` when using file-based approach

## External Dependencies

- **JSZip** (https://stuk.github.io/jszip/) — for ZIP file generation
- **FileSaver.js** (https://github.com/nicolo-ribaudo/FileSaver.js) — for triggering downloads

## Testing Checklist

- [ ] Create project with 10-card list → verify all cards fetched from Scryfall
- [ ] Verify rate limiting works (no 429 errors from Scryfall)
- [ ] Navigate through cards → verify preset is applied to each
- [ ] Upload custom art on card 3 → save project → reload → verify art reference persists
- [ ] Mark cards as done/review → verify status persists
- [ ] Export all → verify ZIP contains correct number of files with correct names
- [ ] Test with 100-card list → verify performance is acceptable
- [ ] Test with multicolor cards → verify correct preset variant is applied
- [ ] Close browser → reopen → load project → verify full state restoration