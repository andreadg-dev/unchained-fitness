# UnchainedFitness

A browser-based training toolkit built around **breaking** (breakdance) conditioning and general strength work. It started as a single HIIT workout builder and has grown into a small multi-section website. Each section has its own purpose and works entirely in the browser, with no backend, no account and no build step.

## Sections

The home page (`index.html`) is a portal with one card per section:

| Section                                    | Folder        | Focus        | What it is for                                                         |
| ------------------------------------------ | ------------- | ------------ | ---------------------------------------------------------------------- |
| [Practice](#practice)                      | `programme/`  | Conditioning | Build a checklist-style workout and tick off each move at your own pace |
| [Time-based Session](#time-based-session)  | `session/`    | Stamina      | Build and run a timed HIIT workout with a guided interval timer        |
| [Strength Training](#strength-training)    | `weights/`    | Strength     | Plan and track a weightlifting programme from your 1RM numbers         |
| [Notes](#notes)                            | `notes/`      | Info         | Reference library of training methods, formats and equipment           |

All sections share the navbar, footer, design tokens and component templates (`global.css`, `components.js`, `paths.js`), so the look and navigation are consistent.

### Practice

Self-paced, checklist-style training.

- Create a new practice, import a shared practice string, or load a saved one
- Add moves from a categorised dropdown, set a repetition count with + / −, and reorder with drag-and-drop
- Mark each exercise complete as you go, with no fixed timer
- Save up to **5 practices** in the browser (`breakingprog_1rm_v0`–`v4`)
- Share a practice as a Base64 string

### Time-based Session

The original HIIT workout builder and timer.

- **Import screen** — create a new workout, paste a shared Base64 workout string, or load a saved session
- **Builder** — add moves, set repetitions, and reorder with drag-and-drop
- **Settings** — active time and rest time per interval (10–120 s), with live totals for exercise count and workout duration
- **Player** — a countdown timer alternating **active** and **rest** phases, with:
  - a breakbeat track during active intervals, fading out on rest
  - the **Screen Wake Lock API** to keep the screen on
  - pause / resume and a volume slider
- Save up to **5 sessions** in the browser (`breakinghiit_1rm_v0`–`v4`)

### Strength Training

A weightlifting planner in the 5/3/1 style (storage key `hardgainers531_1rm_v1`).

- Enter your 1RM for squat, bench press, deadlift and overhead press
- Choose the week (1–3) and training day (A, B, D, E)
- Pick assistance work per day (push, pull, accessory, conditioning)
- The programme for the selected week is calculated from your inputs
- Reset to defaults, clear the stored data, or extract and load your state as a string

### Notes

A static reference library of training methods (for example myoreps and other techniques), competition formats, equipment and practical training notes. Each entry covers how to do it, upsides and downsides.

## Shared features

### Moves and Exercises Overview

Available from the Practice and Time-based Session menus. It is a catalogue of the moves and exercises in `data.js`, shown as expandable cards with a description and a media placeholder. Moves are grouped by category: **Toprock**, **Footwork**, **Freeze**, **PowerMove**, **Conditioning** and **Stretching**.

### Saved Sessions / Practices

Lists the items saved in the browser for the current section. For each one you can:

- View its name, JSON and Base64 string
- Click the Base64 string to copy it
- Delete it

### Save & share

- Sessions and practices are stored in `localStorage` as **Base64-encoded JSON**
- A copied string can be pasted into the Import screen to load the exact same workout
- Names must be between 5 and 15 characters

## Tech stack

| Concern       | Technology                                                  |
| ------------- | ----------------------------------------------------------- |
| Language      | Vanilla JavaScript + jQuery                                 |
| Styling       | Bootstrap 4 (CSS) / Bootstrap 5 (JS), custom CSS per section |
| Drag & drop   | SortableJS                                                  |
| Audio         | HTML5 `<audio>`                                             |
| Screen        | Screen Wake Lock API                                        |
| Storage       | Browser `localStorage`                                      |
| Fonts         | Google Fonts (Inter, Fira Code, Roboto, Montserrat, others) |
| No build step | Plain `.html` / `.js` / `.css`                              |

## Running locally

No build step is needed. Serve the folder with any static server:

```bash
npx serve .
```

You can also open `index.html` directly, but the Wake Lock API requires a secure context (HTTPS or localhost) and audio autoplay policies may apply. Navigation relies on relative paths, so keep the folder structure intact.

## File structure

```
index.html            # Home portal linking to the four sections
index.js              # Shared screen logic for Session and Practice
components.js         # Shared HTML templates, navbar, footer and icons
data.js               # Move/exercise library, storage keys, validation thresholds
paths.js              # Shared path helpers
global.css            # Shared tokens, navbar, footer, overview and saved screens
home.css              # Home portal styles
workout_sample.json   # Example workout JSON payload
CNAME                 # Custom domain for hosting

programme/            # Practice section (index.html, programme.css)
session/              # Time-based Session section (index.html, session.css)
weights/              # Strength Training section (index.html, weights.js, weights.css, data.js)
notes/                # Notes section (index.html, notes.js, notes.css, data.js)
mockups/              # Static design mockups for the screens
audio/                # Breakbeat audio track
images/               # Favicon, portal tiles and brand assets
```

## License

See [LICENSE.txt](LICENSE.txt).
