# Web-Design 2026 — Word Search Game

> **Current game name:** Word Hunt Game

A browser-based word-search puzzle game developed in the context of activities associated with **MPC — Mobile Programming Club** at **Ho Chi Minh City Open University**.

The game lets players find hidden English keywords in a generated letter grid, save progress locally, use hints, play background music, and export the completed result as a PNG image.

## 🎮 Live Demo

[Play Word Hunt Game](https://webdesignwordsearch2026.vercel.app/)

## Features

- 9 × 9 word-search grid
- 5 randomly selected keywords from a pool of 10
- Word placement: right, down, and down-right
- Interactive word selection
- Progress saving with `LocalStorage`
- Replay/reset support
- Timed hints with mascot feedback
- Background music and sound effects
- Victory animation and completion dialog
- PNG result export
- Built-in game guide
- Responsive interface for different screen sizes

## Technology Stack

- HTML5
- CSS3
- JavaScript ES6 Modules
- LocalStorage
- Canvas API
- Web Audio API
- Font Awesome Free 6.4.2
- Google Fonts
- html2canvas-pro 2.3.9

The project is a client-side/static web application. It does not currently use a backend, database, Node.js, or a frontend framework such as React or Vue.

## Game Configuration

The main settings are defined in `js/config.js`.

| Setting           | Value                   |
| ----------------- | ----------------------- |
| Grid size         | 9 × 9                   |
| Keywords per game | 5                       |
| Keyword pool      | 10 words                |
| Directions        | Right, Down, Down-right |
| Reverse words     | Disabled                |
| Hint interval     | 20 seconds              |

Current keyword pool:

`CLINIC`, `SCHOOL`, `FOOD`, `TRAVEL`, `HOUSE`, `SOFTWARE`, `FASHION`, `PHOTO`, `GAME`, `SPORT`

## Project Structure

```text
web-design-2026/
├── index.html
├── README.md
├── AUTHOR.MD
├── .gitignore
├── assets/
│   ├── bg.jpg
│   ├── bgm.webm
│   ├── logo/
│   ├── mascot/
│   └── vendor/
├── content/
│   ├── guide.html
│   └── guide.md
├── css/
│   ├── animation.css
│   ├── game.css
│   ├── popup.css
│   ├── style.css
│   └── welcome.css
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

## Getting Started

No installation or build process is required.

### Using VS Code

Open the project in Visual Studio Code and run `index.html` with a local server such as **Live Server**.

### Using Python

From the project folder:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

A local server is recommended because the project uses ES6 Modules and loads the game guide with `fetch()`.

## How to Play

1. Open the game and press **Play**.
2. Wait for the countdown.
3. Check the keyword list.
4. Select a word by choosing its starting and ending cells.
5. Correct words are highlighted and progress is updated.
6. Find all 5 keywords to complete the game.
7. After winning, use **Save Proof** and **Export Image** if you want to save the result.

## Data & Audio

Game progress is stored locally in the browser using `LocalStorage`. No account or backend is required.

The project also includes background music and sound effects. Audio preferences are handled by the client-side application.

## Repository Context

**Project:** Web-Design 2026 — Word Search Game  
**Current Game Name:** Word Hunt Game  
**Organization:** MPC — Mobile Programming Club  
**University:** Ho Chi Minh City Open University

Official MPC repository:

https://github.com/mpc-ou/minigame.git

## Project Status

**Status:** Educational Project

## License

License information has not been specified in the repository.

## Acknowledgement

Developed in the context of activities associated with **MPC — Mobile Programming Club** at **Ho Chi Minh City Open University**.
