# Web-Design 2026 — Word Search Game

> **Current game name:** Word Hunt Game

A browser-based word-search puzzle game built for the **WEB-DESIGN 2026** project context. The application challenges players to find hidden English keywords in a randomly generated letter grid and provides local progress persistence, timed hints, audio feedback, and PNG result export.

## Project Overview

**Web-Design 2026 — Word Search Game** is the project title. The current game/application name displayed by the implementation is **Word Hunt Game**.

The game is a client-side/static web application. It generates a word-search board in the browser, lets players select words by tapping cells, stores game state in browser `LocalStorage`, and provides a completion workflow for generating and submitting a proof image.

### Organization / Project Context

The project was developed in the context of activities associated with **MPC — Mobile Programming Club** at **Ho Chi Minh City Open University**.

This README does not imply that MPC owns or officially maintains this repository unless separately confirmed by repository metadata.

## Features

The current implementation includes:

- Random generation of a **9 × 9** word-search grid.
- Random selection of **5 keywords** from a pool of 10 configured keywords.
- Random keyword placement in supported directions.
- Interactive cell-by-cell word selection.
- Detection of correctly selected keywords.
- Progress tracking such as `0/5`, `1/5`, and so on.
- Persistent game state using browser `LocalStorage`.
- Resume support for an unfinished or completed saved game.
- Reset/replay functionality that clears the current saved state and creates a new game.
- Timed keyword hints with a mascot-based hint interface.
- Partial keyword masking when a hint is revealed.
- Audio feedback for taps, deselection, successful matches, countdown, hints, and victory.
- Background music with a separate music toggle.
- Custom modal dialogs and a built-in game guide.
- Victory animation with canvas-based confetti.
- Player information input using full name and student ID.
- PNG proof-image generation and download.
- Proof-image preview fallback for in-app browsers or when automatic download is unavailable.
- Optional Google Form submission link after a proof image has been exported.
- Responsive layouts with mobile-specific CSS adjustments.
- Reduced-motion support through `prefers-reduced-motion`.

## Technology Stack

| Technology              | Usage                                                                |
| ----------------------- | -------------------------------------------------------------------- |
| HTML5                   | Page structure and game UI                                           |
| CSS3                    | Layout, styling, responsive behavior, animations, and visual effects |
| JavaScript ES6          | Game logic and browser-side application behavior                     |
| ES6 Modules             | Modular JavaScript organization                                      |
| LocalStorage            | Persistent game state and audio preference storage                   |
| Canvas API              | Victory confetti and generated proof-image rendering                 |
| Web Audio API           | Short sound effects and game audio feedback                          |
| HTMLAudioElement        | Background music playback                                            |
| Font Awesome Free 6.4.2 | Interface icons; bundled locally under `assets/vendor/fontawesome/`  |
| Google Fonts            | Montserrat and VT323 fonts loaded from Google Fonts                  |
| html2canvas-pro 2.3.9   | Converts the proof-image DOM card into a PNG canvas; bundled locally |

There is currently no `package.json`, Node.js backend, database, REST API, framework such as React/Vue/Angular, or bundler in the repository.

## Game Configuration

The main game configuration is defined in `js/config.js`.

| Setting                              | Current value              |
| ------------------------------------ | -------------------------- |
| Grid size                            | `9 × 9`                    |
| Keywords per game                    | `5`                        |
| Keyword pool                         | 10 configured keywords     |
| Word direction                       | Right, Down, Down-right    |
| Reverse words                        | Disabled                   |
| Hint interval                        | 20 seconds                 |
| Hint masking ratio                   | 40%–50% of the target word |
| Urgent hint threshold                | 5 seconds                  |
| Maximum placement attempts per word  | 200                        |
| Maximum matrix regeneration attempts | 50                         |
| Random fill alphabet                 | `A–Z`                      |

### Configured Keyword Pool

The current keyword pool contains:

- `CLINIC`
- `SCHOOL`
- `FOOD`
- `TRAVEL`
- `HOUSE`
- `SOFTWARE`
- `FASHION`
- `PHOTO`
- `GAME`
- `SPORT`

Five keywords are randomly selected from this pool for each newly generated game.

### Word Placement

Words are placed using these directions:

- Right: left → right
- Down: top → bottom
- Down-right: diagonal toward the lower-right

The current configuration does not enable the down-left direction or reverse-word placement.

## Project Structure

```text
web-design-2026/
├── index.html
├── AUTHOR.MD
├── .gitignore
│
├── assets/
│   ├── bg.jpg
│   ├── bgm.webm
│   ├── logo/
│   │   └── logo.png
│   ├── mascot/
│   │   ├── mascot-cheer.png
│   │   ├── mascot-cry.png
│   │   ├── mascot-idle.png
│   │   └── mascot-shy.png
│   └── vendor/
│       ├── html2canvas-pro.min.js
│       └── fontawesome/
│           ├── css/
│           │   └── all.min.css
│           └── webfonts/
│               ├── fa-brands-400.ttf
│               ├── fa-brands-400.woff2
│               ├── fa-regular-400.ttf
│               ├── fa-regular-400.woff2
│               ├── fa-solid-900.ttf
│               └── fa-solid-900.woff2
│
├── content/
│   ├── guide.html
│   └── guide.md
│
├── css/
│   ├── animation.css
│   ├── game.css
│   ├── popup.css
│   ├── style.css
│   └── welcome.css
│
└── js/
    ├── animation.js
    ├── audio.js
    ├── capture.js
    ├── config.js
    ├── game.js
    ├── main.js
    ├── matrix.js
    ├── modal.js
    ├── selection.js
    ├── storage.js
    ├── texts.js
    ├── utils.js
    └── validator.js
```

## Application Architecture

The application is organized as a set of ES6 modules with `js/main.js` acting as the browser entry point.

| Module         | Responsibility                                                                                                                                                                 |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `main.js`      | Initializes the application, restores or creates saved state, switches between screens, connects UI events, manages sound/music controls, loads the guide, and starts the game |
| `config.js`    | Defines grid size, keyword pool, keyword count, directions, storage key, hint settings, placement limits, and Google Form URL                                                  |
| `texts.js`     | Centralizes game names, competition/topic text, modal messages, cover-screen messages, post-win labels, and fallback guide content                                             |
| `game.js`      | Coordinates the main game state, grid rendering, keyword list, selection handling, hints, victory flow, reset, proof workflow, and test-mode helpers                           |
| `matrix.js`    | Generates the grid, selects keywords, places words, and fills remaining cells with random letters                                                                              |
| `selection.js` | Tracks the player's selected cells and restricts selection to configured directions                                                                                            |
| `validator.js` | Compares a selected sequence of letters against active keywords                                                                                                                |
| `storage.js`   | Creates, saves, loads, and clears the main game state in `LocalStorage`                                                                                                        |
| `audio.js`     | Manages sound effects, background music, audio preferences, and Web Audio API tones                                                                                            |
| `animation.js` | Handles cell animations, modal transitions, confetti, hint effects, and the introductory curtain animation                                                                     |
| `capture.js`   | Builds the proof card, renders it through html2canvas-pro, creates a PNG, handles downloads, and provides an image-preview fallback                                            |
| `modal.js`     | Provides reusable alert and confirmation modal dialogs                                                                                                                         |
| `utils.js`     | Provides random values, date formatting, hash generation, cell keys, and keyword masking                                                                                       |
| `validator.js` | Performs keyword-match validation for the current selection                                                                                                                    |

## Getting Started

This is a static web application and does not require a Node.js installation or backend server.

### Option 1 — VS Code Live Server

1. Open the project folder in Visual Studio Code.
2. Install/use a local HTTP server extension such as **Live Server**.
3. Start the server from `index.html`.
4. Open the local address provided by the development server.

### Option 2 — Python HTTP Server

If Python is installed, open a terminal in the project root and run:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

A local HTTP server is recommended instead of opening `index.html` directly with `file://`, because the application uses ES6 modules and also loads `content/guide.html` with `fetch()`.

No `npm install`, build command, or backend startup command is required by the current repository.

## How to Play

1. Open the game and pass the introductory screen, or tap/click it to open it immediately.
2. Press **Play**.
3. A short `3 → 2 → 1 → GO!` countdown starts before a new game.
4. Review the keyword list.
5. Tap a starting cell in the grid.
6. Tap the ending cell of the word to select the sequence.
7. The current implementation accepts horizontal, vertical, and down-right diagonal selections according to the configured directions.
8. Correctly found words are highlighted and the progress counter is updated.
9. Continue until all 5 keywords are found.
10. When the game is completed, the victory dialog, confetti, and post-win controls are displayed.
11. Use **Save Proof** to enter the player's full name and student ID.
12. Use **Export Image** to generate the PNG proof image.
13. If the submission link is available, use **Submit Proof** to open the configured Google Form.

## Hints

The game includes a timed hint system.

- A hint becomes available after **20 seconds**.
- The mascot indicates the hint state and countdown.
- When a hint is used, one not-yet-hinted keyword is selected.
- A partial version of the keyword is revealed by replacing a randomly selected portion of its characters with `_`.
- The masking ratio is currently between **40% and 50%**, while at least one character remains visible.
- The hint timer restarts for another unhinted keyword after a hint is used.
- When all remaining keywords have received hints, the hint interface reports that no hints remain.

The source code and current configuration use a 20-second interval. This is intentionally documented here instead of the older 30-second value that appears in the repository's guide content.

## Data Persistence

The main game state is stored in the browser using `LocalStorage` under the key:

```text
webdesign2026_wordsearch_state
```

The persisted state includes game information such as:

- Generated grid data
- Keyword data
- Word placements
- Found keywords
- Hint state
- Start and completion timestamps
- Completion state
- Player full name and student ID after proof information is submitted
- Proof/export state

Sound and music preferences are also stored separately using:

```text
webdesign2026_sound_enabled
webdesign2026_music_enabled
```

Clearing the game result removes the main saved game state and reloads the application, allowing a new matrix to be generated.

## Audio

The project contains both background music and generated sound effects.

### Background music

The bundled music file is:

```text
assets/bgm.webm
```

Background music can be enabled or disabled independently from sound effects.

### Sound effects

Short tones are generated through the browser's Web Audio API for events including:

- Countdown
- Cell taps
- Cell deselection
- Correct keyword matches
- Victory
- Hint availability
- Hint reveal

The sound and music controls are available on both the cover screen and game screen.

## Export Game Result

After completing the game, the player can enter a full name and a student ID and generate a proof image.

The export implementation:

1. Builds a dedicated proof card in the DOM.
2. Includes the completed grid, game name, topic, player information, completion time, and generated hash.
3. Uses the bundled **html2canvas-pro 2.3.9** library to render the proof card.
4. Creates a PNG image.
5. Attempts a browser download using a generated filename.

The filename follows the pattern:

```text
Minigame-<Full_Name>-<Student_ID>.png
```

If automatic downloading is unavailable, the application displays the generated proof image so the user can save it through a screenshot.

The application also detects several in-app browser user agents, including Facebook, Messenger, Instagram, Zalo, TikTok, and Line, and uses the image-preview/screenshot fallback in those environments.

## Game Guide

The built-in guide is stored in:

```text
content/guide.html
```

The game loads this file dynamically when the guide dialog is opened.

A Markdown version is also provided at:

```text
content/guide.md
```

If loading `content/guide.html` fails, the application falls back to guide content embedded in `js/texts.js`.

## Browser Compatibility

The game is intended for modern browsers that support the web platform features used by the application, including:

- ES6 JavaScript
- ES6 Modules
- `LocalStorage`
- Canvas
- Web Audio API
- Modern CSS
- `fetch()`
- Standard HTML audio playback

The project includes responsive CSS rules for smaller screens, including specific adjustments for viewport widths of `480px` or less and shorter viewport heights.

No browser-specific guarantee is made by the project. Testing in a current version of a modern browser is recommended.

## Responsive Design

The CSS implementation includes responsive adjustments for smaller devices.

The game provides:

- Mobile-oriented control sizing
- Safe-area-aware positioning for fixed controls
- Smaller grid/UI spacing on narrow screens
- Adjustments for short viewport heights
- Layout behavior intended for desktop, laptop, tablet, and mobile-sized screens

The repository does not claim universal or perfect responsive compatibility across every device.

## Privacy and Data Handling

The application is primarily client-side and does not contain a backend or database.

Game state is stored locally in the user's browser. The application also asks the player to enter a full name and student ID when creating a proof image; those values are stored in the local game state and are included in the generated proof image.

The application contains an optional external Google Form submission flow. When the player chooses to submit proof through that flow, information is submitted to the external form configured in `js/config.js`.

The repository therefore should not be interpreted as providing a general privacy or data-protection guarantee beyond the behavior visible in the current source code.

## Repository Relationship

The official MPC repository referenced by the project context is:

**https://github.com/mpc-ou/minigame.git**

This project is associated with the MPC project context at **Ho Chi Minh City Open University**.

The available project source does not contain Git remote metadata establishing that this repository is a fork of the official MPC repository or that the two repositories are identical. Therefore, this README does not describe it as a fork or identical copy.

## Development Workflow

The project can be developed using normal Git workflows.

Example:

```bash
git clone <repository-url>
cd web-design-2026

git status
git add .
git commit -m "Describe your changes"
git push origin main
```

`<repository-url>` is intentionally left as a placeholder because the provided project source does not contain a confirmed Git remote URL.

## Commit Convention

The repository does not define a formal commit-message convention. The following are examples of clear commit messages:

```text
Add new game feature
Fix word placement logic
Update responsive layout
Improve game UI
Add audio controls
Update game configuration
Fix mobile interaction
Update documentation
```

These examples are suggestions, not official project rules.

## Testing Checklist

Before publishing changes, manually verify the features supported by the current implementation:

- [ ] Game loads through a local HTTP server.
- [ ] Introductory screen opens normally.
- [ ] Play flow and countdown work.
- [ ] A 9 × 9 grid is generated.
- [ ] Five keywords are selected for a new game.
- [ ] Keywords are placed in the configured directions.
- [ ] Cell selection follows the configured direction rules.
- [ ] Correct words are detected and highlighted.
- [ ] Progress updates correctly.
- [ ] Game state persists after reload.
- [ ] An unfinished game can be resumed.
- [ ] Reset/replay creates a fresh game.
- [ ] Timed hints become available.
- [ ] Hint masking works.
- [ ] Sound effects can be toggled.
- [ ] Background music can be toggled.
- [ ] Victory dialog and confetti appear after all keywords are found.
- [ ] Full name and student ID validation works.
- [ ] PNG proof generation works.
- [ ] Proof image download works in a normal browser.
- [ ] Proof-image fallback works when automatic download is unavailable.
- [ ] Google Form submission flow opens correctly when configured.
- [ ] The built-in guide loads from `content/guide.html`.
- [ ] No unexpected browser console errors appear during normal use.
- [ ] The interface remains usable on narrow and short viewports.

## Technical Considerations

### Static Client-Side Architecture

All core game logic executes in the browser. There is no application server or database in the repository.

### Modular JavaScript

The code is separated into ES6 modules for configuration, game state, matrix generation, selection, validation, storage, audio, animation, dialogs, proof generation, and utility functions.

### Randomized Game Generation

A new game randomly selects five keywords from the configured pool and attempts to place them in a newly generated 9 × 9 grid. Empty cells are filled with random uppercase letters.

### Saved State Validation

On startup, the application validates the saved grid and keyword-placement structure before using it. Invalid or missing saved state results in a newly generated game.

### Proof Generation

The proof image is generated from a temporary DOM structure rather than simply capturing the visible game screen. The generated structure is rendered at a fixed `540 × 720` logical size and converted to PNG through the bundled html2canvas-pro library.

### Test Mode

`TEST_MODE` is currently set to `true` in `js/config.js`.

The current implementation includes hidden test shortcuts:

- Clicking the game-screen sound button five times within five seconds triggers the game's `autoSolve()` helper.
- Clicking the game-screen music button five times within five seconds triggers `revealAllHints()`.

These are implementation details of the current source and should be considered when testing or deploying the application.

## Project Status

**Status: Educational Project**

The repository contains a functional browser-based word-search game implementation intended for the WEB-DESIGN 2026 project context.

## License

No `LICENSE` file or explicit project license information is present in the provided repository.

**License information has not been specified in the repository.**

The repository does contain bundled third-party assets with their own license information. For example, the bundled Font Awesome Free files identify their applicable Font Awesome licenses, and html2canvas-pro identifies an MIT license in its distributed file header. These third-party licenses should be considered separately from the project itself.

## Project Context

| Item                       | Information                            |
| -------------------------- | -------------------------------------- |
| Project                    | Web-Design 2026 — Word Search Game     |
| Current Game Name          | Word Hunt Game                         |
| Organization               | MPC — Mobile Programming Club          |
| University                 | Ho Chi Minh City Open University       |
| Project Context Repository | `BapDev06/web_design_wordsearch_2026`  |
| Official MPC Repository    | https://github.com/mpc-ou/minigame.git |

## Acknowledgement

This project was developed in the context of activities associated with **MPC — Mobile Programming Club** at **Ho Chi Minh City Open University**.

The repository also includes author information identifying **BapDev06** as the project author.

---

## Author

According to `AUTHOR.MD`:

- **Full Name:** Ngô Nhật Tuấn
- **GitHub:** BapDev06
- **Project Name:** Word Hunt Game
