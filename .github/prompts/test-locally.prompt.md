# Test All Features Locally

## Task

Run comprehensive local testing of all implemented features before committing.

## Setup

1. Start local server: `python -m http.server 8000` or `docker compose up`
2. Open browser to `http://localhost:8000` (or `:4242` for Docker)
3. Open browser DevTools console to monitor for errors

## Test Suite

### Regression Tests (Existing Functionality)
- [ ] Load app without errors
- [ ] Create a card manually (select frame, upload art, add text)
- [ ] Import a card from Scryfall by name
- [ ] Download a single card as JPEG
- [ ] Save/load a card via existing JSON mechanism

### Preset System Tests
- [ ] Create a card with extended art green frame, set symbol, watermark, collector info
- [ ] Save as preset "Test Set - Green"
- [ ] Generate color variants → verify 9 variants created
- [ ] Load blue variant → verify frames changed correctly
- [ ] Import "Counterspell" from Scryfall with preset active → verify blue variant auto-applied
- [ ] Export preset pack as JSON file
- [ ] Clear localStorage → import preset JSON → verify restoration
- [ ] Delete a preset → verify it's removed from list and storage

### Project Manager Tests
- [ ] Create new project "Test Deck" with preset pack
- [ ] Import 10-card list (mix of colors, including multicolor and artifacts)
- [ ] Verify Scryfall fetch completes without errors
- [ ] Navigate through all 10 cards → verify correct preset variant on each
- [ ] On card 3: upload custom art, adjust position, mark as Done
- [ ] On card 5: add custom flavor text color override
- [ ] Save project → close tab → reopen → load project → verify all state
- [ ] Export all → verify ZIP download with 10 correctly named PNG files
- [ ] Verify exported images render correctly (open in image viewer)

### Edge Cases
- [ ] Import a card that doesn't exist on Scryfall → verify graceful error
- [ ] Create project with 0 cards → verify no crash
- [ ] Try to export project with no completed cards → verify appropriate message
- [ ] Test with very long card names (e.g., "Our Market Research Shows That Players Like Really Long Card Names So We Made this Card to Have the Absolute Longest Card Name Ever Elemental")
- [ ] Test with split/double-faced cards → verify handling

### Performance Tests
- [ ] Import 100-card list → measure time to fetch all from Scryfall
- [ ] Export 100 cards → measure time and verify no browser freeze (should use async rendering)
- [ ] Verify localStorage doesn't exceed browser limits with large projects

## Report

After testing, create `TEST_RESULTS.md` with:
- Pass/fail status for each test
- Any bugs found with reproduction steps
- Performance measurements
- Screenshots of any visual issues
- Suggestions for improvements based on testing experience