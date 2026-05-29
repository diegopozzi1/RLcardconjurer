# Implement Preset System

## Prerequisites

- [ ] `IMPLEMENTATION_PLAN.md` has been reviewed and approved
- [ ] Feature branch `feature/preset-system` is active
- [ ] Codebase analysis is complete

## Task

Implement the Preset System as described in the implementation plan.

## Implementation Steps

1. **Create `js/presets.js` module**
   - Define the Preset data structure (JSON schema)
   - Implement `savePreset(name, cardState)` — captures current card configuration
   - Implement `loadPreset(presetName)` — applies preset to canvas
   - Implement `generateColorVariants(basePreset)` — creates W/U/B/R/G/M/C/Land/Token variants
   - Implement `detectColorAndApplyPreset(scryfallData, presetPack)` — auto-applies based on color identity
   - Implement `exportPreset(preset)` / `importPreset(jsonFile)` — file I/O

2. **Create Preset UI**
   - Add "Presets" tab/section to the existing interface
   - "Save Current as Preset" button with name input
   - "Generate Color Variants" button (after saving a base preset)
   - Preset list with load/delete/export actions
   - Import preset button (file picker for JSON)

3. **Integrate with Scryfall Import**
   - Hook into existing card import flow
   - After Scryfall data is loaded, check if a preset pack is active
   - If yes, auto-apply the matching color variant
   - Auto-increment collector number

4. **Persistence**
   - Save presets to localStorage as primary storage
   - Provide JSON export/import for backup and sharing
   - Store in `data/presets/` when using file-based approach

## Testing Checklist

- [ ] Save a green creature preset → verify JSON structure is complete
- [ ] Generate color variants → verify all 9 variants are created with correct frames
- [ ] Load a preset → verify canvas renders correctly
- [ ] Import a card via Scryfall with active preset → verify auto-application
- [ ] Export preset → re-import → verify identical behavior
- [ ] Close browser → reopen → verify presets persist in localStorage