# Daggerheart-Compatible Single-Page Character Creator — Build Plan

**File purpose:** Planning document for building a full-featured online character creator as a single `index.html` file that can be hosted on GitHub Pages.

**Recommended public app name:** Do **not** put “Daggerheart” in the product title/logo unless the current Darrington Press Community Gaming License allows your exact usage. Use a neutral title such as **Heartforge Character Builder** with subtitle text like “compatible with Daggerheart™” if compliant.

**Target format:** One self-contained HTML file with embedded CSS and JavaScript.

**Target host:** GitHub Pages.

**Primary goal:** Let a player create, validate, save, print, export, import, level up, and manage a Daggerheart-compatible character without needing a backend server.

---

## 1. Ground Rules and Licensing Guardrails

Before publishing, review the current official Daggerheart SRD and Darrington Press Community Gaming License.

Implementation should assume the following guardrails unless you get explicit permission or the current license says otherwise:

1. Build from the official SRD/public game content, not the full commercial rulebook.
2. Do not include scanned pages, official card images, official art, official logos, or proprietary layout assets.
3. Do not copy large blocks of card/rule text unless that exact text is licensed for reuse.
4. Include required attribution and compatibility language from the current license.
5. Treat the application as an independent fan/community tool, not official or endorsed.
6. Allow custom/user-entered data packs so users can add content they personally own without the app distributing protected material.
7. Store all characters locally by default to avoid collecting user data.

Useful official references to review while implementing:

- Daggerheart SRD: https://www.daggerheart.com/srd/
- Darrington Press Community Gaming License: https://darringtonpress.com/license/
- Official Downloads page: https://www.daggerheart.com/downloads/

---

## 2. Product Vision

Build a fast, mobile-friendly, no-login character creator that feels like a guided wizard and a live character sheet at the same time.

The app should support:

- First-time guided character creation.
- Expert free-edit mode.
- Validation against SRD rules.
- Autosaved local characters.
- Import/export as JSON.
- Printable character sheet.
- Shareable character file.
- Optional homebrew data packs.
- Level-up and advancement tracking.
- Accessibility and offline-friendly design.

The finished app should be easy to host by uploading one `index.html` file to a GitHub Pages repository.

---

## 3. Recommended Technical Approach

### 3.1 Architecture

Use **vanilla HTML, CSS, and JavaScript** inside one file.

Avoid a build step. Avoid server-side code. Avoid databases. Avoid frameworks unless you are comfortable accepting CDN dependency risk.

Suggested structure inside `index.html`:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Heartforge Character Builder</title>
  <style>
    /* App styles */
  </style>
</head>
<body>
  <noscript>This character builder requires JavaScript.</noscript>
  <main id="app"></main>
  <script>
    // Data, state, renderer, validation, import/export, and utilities.
  </script>
</body>
</html>
```

### 3.2 Main JavaScript Modules Inside One File

Keep the code organized with named objects or functions:

```js
const AppConfig = {};
const SRDData = {};
const DefaultHomebrewData = {};
const State = {};
const Store = {};
const Rules = {};
const Validators = {};
const Renderer = {};
const Components = {};
const ImportExport = {};
const PrintTools = {};
const Utilities = {};
```

### 3.3 Persistence

Use browser storage only:

- `localStorage` for simple saved characters and settings.
- `IndexedDB` only if you want larger data packs, character portraits, or many saved characters.
- Exportable `.json` files for long-term backups.

### 3.4 Data Strategy

Use internal JSON-style data objects. Keep official/SRD data separated from user/homebrew data.

Recommended layers:

1. **Core rules metadata** — traits, damage types, card slots, level structure, etc.
2. **SRD content pack** — only content allowed by the SRD/license.
3. **User homebrew pack** — user-created classes, subclasses, ancestries, communities, equipment, cards, and rules variants.
4. **Character save file** — only a player’s selected choices and notes.

---

## 4. Main User Modes

### 4.1 Guided Builder Mode

A wizard-style flow for new characters.

Recommended steps:

1. Welcome and license/disclaimer.
2. Character concept.
3. Class and subclass.
4. Heritage: ancestry and community.
5. Trait assignment.
6. Starting character information.
7. Starting equipment.
8. Background and description.
9. Experiences.
10. Domain/card choices.
11. Connections.
12. Review and validation.
13. Final character sheet.

### 4.2 Sheet Mode

A live, editable character sheet for play.

Should include:

- Character identity.
- Traits.
- Hope/Fear-related notes.
- Hit points, stress, armor, thresholds, evasion, and resources.
- Active weapons.
- Active armor.
- Inventory.
- Experiences.
- Domain cards/loadout.
- Class/subclass/heritage features.
- Connections.
- Notes.
- Level and advancement.

### 4.3 Expert Edit Mode

Allow direct edits and overrides for experienced players, GMs, and homebrew.

Features:

- Manual stat overrides.
- Rule warnings instead of hard blocks.
- Custom feature text fields.
- Add/remove arbitrary cards.
- Custom equipment.
- Custom conditions/status notes.
- GM-approved house rule toggles.

### 4.4 Library/Data Manager Mode

Manage content packs.

Features:

- View installed data packs.
- Import data pack JSON.
- Export homebrew pack.
- Enable/disable packs.
- Search all content.
- Detect conflicting IDs.
- Show license/source metadata per pack.

---

## 5. Full Feature Checklist

### 5.1 Character Identity

- Character name.
- Pronouns.
- Player name.
- Campaign name.
- Party name.
- Character portrait upload or URL.
- Portrait crop/position controls.
- Short concept field.
- Long description field.
- Personality tags.
- Ideals, flaws, bonds, fears, goals.
- Voice/mannerism notes.
- Background questions.
- Private notes.
- Public notes.

### 5.2 Class and Subclass Selection

- Class list with filters.
- Subclass list based on class.
- Feature preview.
- Domain access preview.
- Spellcast trait display when relevant.
- “Why choose this?” summary written in original app text.
- Required choices prompted immediately.
- Support for class-specific side panels.
- Support for future/new classes via data packs.
- Support for multiclassing as an advanced feature.

### 5.3 Heritage Selection

- Ancestry selection.
- Community selection.
- Feature preview.
- Trait/theme tags.
- Appearance prompts.
- Culture/upbringing prompts.
- Homebrew ancestry/community creator.
- Compatibility validator for missing required features.

### 5.4 Trait Assignment

- Drag-and-drop or dropdown assignment.
- Display legal starting array.
- Warnings for duplicate/missing values.
- Manual override toggle.
- “Recommend traits for my concept” helper.
- Randomize legal distribution.
- Explain what each trait is used for in original summary language.

### 5.5 Derived Stats and Resources

- Starting level.
- Hope tracker.
- Stress tracker.
- Hit point tracker.
- Armor score.
- Evasion.
- Damage thresholds.
- Proficiency or equivalent scaling if used by the current rules.
- Severe/major/minor damage display if applicable.
- Automatic recalculation when equipment, level, or features change.
- Manual override for each derived value.
- Change log showing why a value is what it is.

### 5.6 Equipment Builder

- Starting weapon selection.
- Active weapon slots.
- Weapon trait display.
- Weapon range display.
- Weapon burden/feature fields if applicable.
- Damage dice display.
- Physical/magic damage support.
- Starting armor selection.
- Armor threshold calculation.
- Inventory editor.
- Gold/currency or campaign resource tracker.
- Loadout presets.
- Custom item builder.
- Search/filter equipment by trait, damage, range, tier, or tags.

### 5.7 Experiences

- Create two starting experiences.
- Default modifier fields.
- Validation for blank/broad/game-breaking entries with soft warnings.
- Experience usage notes.
- Add/upgrade experiences during advancement.
- Tag experiences by social, combat, exploration, knowledge, craft, magic, etc.
- Quick “spend Hope to use” reminder if allowed by current rules.

### 5.8 Domain Cards / Ability Cards

- Domain list.
- Card level/tier filters.
- Search by name, domain, level, cost, action type, tags.
- Loadout vs vault view.
- Drag-and-drop card management.
- Validation for legal selections.
- Custom card creator.
- Card print layout.
- “Do not distribute protected card text” data policy.
- Import user-owned card data.
- Toggle short/original app summaries vs full user-entered text.

### 5.9 Connections

- Guided connection prompts.
- Party member list.
- Connection question fields.
- Relationship map.
- Session zero notes.
- Shared backstory links.
- Consent/safety notes visible only to player if desired.

### 5.10 Level-Up and Advancement

- Current level.
- Advancement checklist.
- Available upgrades by level/tier.
- Feature unlock prompts.
- Domain/card unlock prompts.
- Experience upgrade support.
- Trait/stat upgrade support if applicable.
- Hit point/stress/resource changes.
- Multiclass sheet support.
- Level history log.
- Undo level-up.
- Compare previous vs current level.

### 5.11 Play Mode

- Large resource trackers for table use.
- One-click mark/unmark HP/stress/armor/resource boxes.
- Roll helper for Duality Dice.
- Hope/Fear result display.
- Advantage/disadvantage or modifier support if applicable.
- Dice history log.
- Custom roll buttons based on traits/weapons/experiences.
- Session notes.
- Condition/status tracker.
- Short rest/long rest or downtime buttons if applicable.
- “Table-safe” mode that hides spoilers/private notes.

### 5.12 Export, Import, Sharing, and Printing

- Save to browser.
- Duplicate character.
- Rename character.
- Delete with confirmation.
- Export character as `.json`.
- Import character `.json`.
- Export all characters.
- Import backup bundle.
- Copy share code to clipboard.
- Import from share code.
- Browser print stylesheet.
- Print compact sheet.
- Print full sheet.
- Print cards/loadout.
- Optional export to image using browser APIs.
- Optional export to PDF through browser print, not a server.

### 5.13 Search and Usability

- Global search.
- Filterable lists.
- Favorites.
- Recently used options.
- Tooltips.
- Contextual help.
- Progress tracker.
- Validation summary.
- Unsaved change warning.
- Undo/redo stack.
- Keyboard shortcuts.
- Mobile-first responsive design.
- Dark/light mode.
- High contrast mode.

### 5.14 Accessibility

- Semantic HTML.
- Keyboard navigation.
- Visible focus states.
- Proper labels for every input.
- ARIA only where useful.
- Color is not the only meaning carrier.
- Screen-reader-friendly validation messages.
- Respect reduced motion.
- Large tap targets.
- Print-friendly contrast.

### 5.15 Privacy and Security

- No analytics by default.
- No external tracking.
- No account required.
- Characters stay in the browser unless exported/shared.
- Sanitize imported JSON text before rendering.
- Never render imported HTML as trusted markup.
- Escape all user-entered text.
- Confirm before deleting local saves.
- Include backup reminder.

### 5.16 GM/Party Extras

These are optional, but useful:

- Party roster.
- Import multiple characters.
- Campaign dashboard.
- Shared connection map.
- Party resource summary.
- Session notes export.
- GM view that hides private player notes.
- Encounter/adversary tracker later, if scope expands.

---

## 6. Data Model Draft

### 6.1 Character Save Schema

Use a versioned schema so older character files can be migrated.

```js
const character = {
  schemaVersion: "1.0.0",
  appVersion: "0.1.0",
  id: "char_20260706_abc123",
  createdAt: "2026-07-06T00:00:00.000Z",
  updatedAt: "2026-07-06T00:00:00.000Z",
  identity: {
    name: "",
    pronouns: "",
    playerName: "",
    campaignName: "",
    concept: "",
    description: "",
    portraitDataUrl: ""
  },
  build: {
    level: 1,
    classId: "",
    subclassId: "",
    ancestryId: "",
    communityId: "",
    multiclass: []
  },
  traits: {
    agility: null,
    strength: null,
    finesse: null,
    instinct: null,
    presence: null,
    knowledge: null
  },
  resources: {
    hope: 2,
    stressMarked: 0,
    hpMarked: 0,
    armorMarked: 0
  },
  derived: {
    evasion: null,
    armorScore: null,
    thresholds: {
      major: null,
      severe: null
    }
  },
  equipment: {
    activeWeapons: [],
    activeArmor: null,
    inventory: []
  },
  experiences: [],
  cards: {
    loadout: [],
    vault: [],
    custom: []
  },
  features: {
    selectedOptions: {},
    customFeatures: []
  },
  connections: [],
  notes: {
    public: "",
    private: "",
    sessionLog: []
  },
  settings: {
    rulesMode: "srd",
    allowOverrides: false,
    enabledPacks: []
  }
};
```

### 6.2 Content Pack Schema

```js
const contentPack = {
  schemaVersion: "1.0.0",
  id: "srd-core-or-homebrew-pack-id",
  name: "Pack Name",
  author: "Author Name",
  license: "License name or private-use only",
  sourceUrl: "",
  version: "1.0.0",
  classes: [],
  subclasses: [],
  ancestries: [],
  communities: [],
  domains: [],
  cards: [],
  weapons: [],
  armor: [],
  items: [],
  rulesVariants: []
};
```

### 6.3 Example Content Object Shape

Use IDs instead of names for saved references.

```js
const exampleClass = {
  id: "class_example",
  name: "Example Class",
  summary: "Original short description written for this app.",
  domains: ["domain_a", "domain_b"],
  features: [
    {
      id: "feature_example",
      name: "Example Feature",
      text: "Only include text you are licensed to include."
    }
  ],
  starting: {
    evasion: null,
    inventory: [],
    choices: []
  }
};
```

---

## 7. Validation System

Build validation as warnings and errors.

### 7.1 Errors

Errors block “character complete” status.

Examples:

- No class selected.
- No subclass selected.
- No ancestry selected.
- No community selected.
- Trait array is incomplete.
- Required class/subclass choice missing.
- Required equipment choice missing.
- Required starting experiences missing.
- Illegal number of loadout cards.

### 7.2 Warnings

Warnings allow completion but ask the user to review.

Examples:

- Experience may be too broad.
- Custom content has no source/license metadata.
- Manual override enabled.
- Character uses disabled content pack.
- Imported file was created with a newer app version.
- Character has private notes that will appear in print/export.

### 7.3 Validation Output

Show validation in three places:

1. Step-level status badges.
2. Review page checklist.
3. Sheet mode banner.

---

## 8. UI Layout Plan

### 8.1 Desktop Layout

Use a two-column layout:

- Left: builder controls.
- Right: live character sheet preview.

Top navigation:

- Build
- Sheet
- Cards
- Equipment
- Level Up
- Notes
- Library
- Settings

### 8.2 Mobile Layout

Use stacked cards and a sticky bottom nav:

- Build
- Sheet
- Resources
- Cards
- More

### 8.3 Visual Design

Keep the design original. Avoid copying official character sheet or card layouts.

Suggested design direction:

- Clean fantasy dashboard.
- Neutral parchment-like optional theme, but not official art.
- Simple card components.
- Large touch-friendly trackers.
- Distinct warning/error colors.
- Compact print mode.

---

## 9. Core Functions to Implement

### 9.1 App Initialization

```js
function initApp() {
  loadSettings();
  loadContentPacks();
  loadCharacters();
  bindGlobalEvents();
  render();
}
```

### 9.2 State Updates

```js
function updateCharacter(path, value) {
  setByPath(State.currentCharacter, path, value);
  State.currentCharacter.updatedAt = new Date().toISOString();
  recalculateCharacter(State.currentCharacter);
  validateCharacter(State.currentCharacter);
  saveCurrentCharacter();
  render();
}
```

### 9.3 Recalculation

```js
function recalculateCharacter(character) {
  applyBaseRules(character);
  applyClassFeatures(character);
  applyHeritageFeatures(character);
  applyEquipment(character);
  applyCards(character);
  applyOverrides(character);
  return character;
}
```

### 9.4 Import Safety

```js
function safeImportCharacter(jsonText) {
  const parsed = JSON.parse(jsonText);
  assertValidCharacterSchema(parsed);
  migrateIfNeeded(parsed);
  sanitizeUserText(parsed);
  return parsed;
}
```

---

## 10. GitHub Pages Deployment Plan

### 10.1 Repository Setup

1. Create a new GitHub repository.
2. Add `index.html`.
3. Add `README.md`.
4. Add `LICENSE` for your own code.
5. Add `NOTICE.md` for Daggerheart compatibility attribution if required by the current license.
6. Commit and push.
7. Go to repository **Settings → Pages**.
8. Set source to the main branch and root folder.
9. Publish.

### 10.2 Single-File Rule

For strict single-file hosting, keep everything in `index.html`:

- CSS in `<style>`.
- JavaScript in `<script>`.
- SVG icons inline.
- No external fonts unless acceptable.
- No images except user-uploaded portraits stored locally.

### 10.3 Optional Non-Single-File Enhancements

These are useful later but break the strict single-file goal:

- `manifest.webmanifest` for PWA install.
- `service-worker.js` for offline caching.
- Separate JSON content packs.
- Separate test files.
- Separate CSS/JS for maintainability.

---

## 11. Implementation Roadmap

### Phase 0 — Legal/Content Prep

Deliverables:

- Confirm current SRD/CGL requirements.
- Decide exact public app name.
- Write attribution/disclaimer text.
- Decide what SRD content can be bundled.
- Decide what must be user-imported only.

Exit criteria:

- You know what content is safe to include.
- You have required notice text ready.

### Phase 1 — App Skeleton

Deliverables:

- `index.html` with responsive shell.
- App state object.
- Local storage save/load.
- Navigation tabs.
- Empty character creation.
- Basic settings panel.

Exit criteria:

- A character can be created, saved, reopened, renamed, duplicated, and deleted.

### Phase 2 — Guided Character Creation MVP

Deliverables:

- Identity step.
- Class/subclass step.
- Heritage step.
- Trait assignment step.
- Equipment step.
- Background step.
- Experiences step.
- Connections step.
- Review checklist.

Exit criteria:

- A level 1 character can be completed with validation.

### Phase 3 — Live Character Sheet

Deliverables:

- Sheet mode.
- Resource trackers.
- Derived stat calculations.
- Feature summaries.
- Inventory editor.
- Print stylesheet.

Exit criteria:

- The app is usable during a game session.

### Phase 4 — Cards and Loadout System

Deliverables:

- Domain/card browser.
- Loadout/vault management.
- Search and filters.
- Custom card creator.
- Card validation.
- Print loadout.

Exit criteria:

- A player can manage legal card choices and custom/homebrew cards.

### Phase 5 — Import/Export and Data Packs

Deliverables:

- Character export/import.
- Full backup export/import.
- Content pack import/export.
- Pack conflict detection.
- Migration system.
- Sanitization of imported data.

Exit criteria:

- Characters and homebrew can survive browser/device changes.

### Phase 6 — Level-Up and Advanced Rules

Deliverables:

- Level-up wizard.
- Advancement checklist.
- Level history.
- Multiclass support.
- Manual overrides.
- House rule toggles.

Exit criteria:

- A campaign character can be maintained long-term.

### Phase 7 — Polish and Public Release

Deliverables:

- Mobile polish.
- Accessibility pass.
- Keyboard navigation.
- Help text.
- Error handling.
- README.
- GitHub Pages deploy.
- Beta feedback form link if desired.

Exit criteria:

- Public beta is ready.

---

## 12. Testing Plan

### 12.1 Manual Test Characters

Create at least these test cases:

1. Standard level 1 character with no overrides.
2. Character with all custom notes and portrait.
3. Character with custom equipment.
4. Character with custom/homebrew cards.
5. Character using manual stat overrides.
6. Imported character from old schema version.
7. Character with missing required choices.
8. Max-length text stress test.
9. Mobile viewport test.
10. Print layout test.

### 12.2 Browser Tests

Test in:

- Chrome.
- Firefox.
- Safari.
- Edge.
- iOS Safari.
- Android Chrome.

### 12.3 Accessibility Tests

- Keyboard-only creation.
- Screen reader labels.
- High contrast mode.
- Browser zoom at 200%.
- Reduced motion.

### 12.4 Import/Security Tests

- Invalid JSON.
- Missing schema version.
- Unsupported future schema version.
- Huge imported file.
- HTML/script injection inside character notes.
- Duplicate content pack IDs.

---

## 13. Suggested MVP Scope

If you want to actually finish the first version quickly, build this first:

1. One character at a time.
2. Level 1 only.
3. Manual content entry instead of bundled official card text.
4. Class/subclass/heritage selectors with summary fields.
5. Trait assignment validation.
6. Equipment editor.
7. Experiences and connections.
8. Local autosave.
9. JSON export/import.
10. Print stylesheet.

Then add the advanced systems after the foundation works.

---

## 14. Nice-to-Have Future Features

- AI-free random concept generator using local tables.
- Custom campaign templates.
- Session recap fields.
- Party relationship graph.
- QR code share/export.
- Cloud sync using user-provided GitHub Gist token.
- Optional Google Drive export, if you later add OAuth.
- Dice probability helper.
- Theme editor.
- Homebrew marketplace-style pack directory, if legally allowed.
- GM approval workflow for imported homebrew.
- Encounter tracker as a separate mode.
- Companion, familiar, beastform, or sidecar sheets.
- Multiple print templates.
- Compact index-card print mode.
- “Table mode” with huge resource buttons.

---

## 15. Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Accidentally distributing protected text/art | Use SRD only, avoid official scans/card images, let users import private data |
| License changes | Add a release checklist to review the current DPCGL before publishing updates |
| Single-file becomes hard to maintain | Keep code sections clearly labeled; later split source files for development and build into one file |
| Browser storage loss | Prominent export/backup reminders |
| Import files cause XSS | Treat imported data as plain text; escape all rendered content |
| Rules complexity | Build manual override mode and clear validation warnings |
| Mobile layout becomes cluttered | Use progressive disclosure and sticky resource controls |
| Print layout is ugly | Make print CSS a dedicated milestone |

---

## 16. Definition of Done for Public Beta

The public beta is ready when:

- The app works from a single `index.html` on GitHub Pages.
- Users can complete a level 1 character.
- Characters autosave locally.
- JSON export/import works.
- Print view is readable.
- Validation catches missing required choices.
- Mobile layout is usable.
- Attribution/disclaimer text is present.
- No official art, scans, or non-permitted copied text is bundled.
- README explains that characters are stored locally and users should export backups.

---

## 17. README Draft

```md
# Heartforge Character Builder

A single-page, browser-based character builder compatible with Daggerheart™.

This is an independent community tool and is not official or endorsed by Darrington Press or Critical Role.

## Features

- Guided character creation
- Live character sheet
- Local autosave
- JSON import/export
- Print-friendly layout
- Homebrew/custom content support

## Privacy

Characters are stored in your browser by default. Export backups regularly.

## Hosting

Upload `index.html` to a GitHub Pages repository and enable Pages in repository settings.

## Content and Licensing

This project is intended to use only content permitted by the official Daggerheart SRD and the Darrington Press Community Gaming License. Review the current license before publishing or distributing changes.
```

---

## 18. First Coding Sprint Checklist

Use this checklist when you start implementing:

- [ ] Create `index.html`.
- [ ] Add responsive app shell.
- [ ] Add `State.currentCharacter`.
- [ ] Add create/save/load/delete character functions.
- [ ] Add identity form.
- [ ] Add class/subclass fields.
- [ ] Add ancestry/community fields.
- [ ] Add trait assignment UI.
- [ ] Add equipment fields.
- [ ] Add experiences fields.
- [ ] Add connections fields.
- [ ] Add validation summary.
- [ ] Add sheet preview.
- [ ] Add export JSON.
- [ ] Add import JSON.
- [ ] Add print CSS.
- [ ] Add attribution/disclaimer block.
- [ ] Test on GitHub Pages.

---

## 19. Recommended Build Order Inside the Single HTML File

1. Global CSS variables and layout.
2. Static app shell.
3. Data constants.
4. Default character factory.
5. Storage layer.
6. Validation layer.
7. Calculation layer.
8. Rendering helpers.
9. Builder components.
10. Sheet components.
11. Import/export tools.
12. Print CSS.
13. Event listeners.
14. `initApp()` call.

---

## 20. Final Product Philosophy

Make the builder helpful without pretending to replace the game book. It should guide players, organize choices, prevent obvious mistakes, and make the character easy to use at the table. Keep the app original, clean, privacy-respecting, and easy to fork.
