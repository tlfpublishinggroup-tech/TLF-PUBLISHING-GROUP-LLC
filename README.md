# TLF-PUBLISHING-GROUP-LLC
TLF CORE SHELL

## Data Files Architecture

All app data is now stored in `data/*.json` files in the repository instead of being embedded in `index.html`. This prevents browser storage quota issues ("site full" in Safari) and makes the app safe to use with large datasets (700+ tracks).

### Data file locations

| File | Contents |
|---|---|
| `data/home.json` | Home tab text (about, vision, mission) |
| `data/books.json` | Books tab data (BOOK-01 … BOOK-18) |
| `data/music.json` | Music grid artists, logo boxes, and track lists |
| `data/videos.json` | Videos categories and playlists |
| `data/movies.json` | Movies posters, YouTube player URL |
| `data/more.json` | About Us, Careers, Terms, Conditions, Privacy, Policy |

### How the loading priority works

1. **`data/*.json`** files are fetched from the repository when the app loads (base layer).
2. **Browser localStorage** edits are merged on top (your in-app changes always win).
3. If a JSON file is missing or unreachable, the app falls back to its built-in defaults — nothing breaks.

### How to deploy updated data

1. Export the tab JSON from the app (e.g. "EXPORT BOOKS").
2. Rename and paste the contents into the matching `data/*.json` file in the repo.
3. Commit and push (or open a PR and merge).
4. **Hard refresh** the live site (`Cmd+Shift+R` / `Ctrl+Shift+R`) to bypass the browser cache and pick up the new data.

### Caveats

- **Browser cache**: After updating a data file in the repo, do a hard refresh on the live site to see changes.
- **localStorage still works**: Any edits you make inside the app are saved to localStorage and take precedence over the repo files. This means your in-app changes are never overwritten by a data file update.
- **Large track lists**: For 700+ tracks, split the data across multiple music logo entries (each logo box holds its own track array inside `data/music.json`).
- **Images**: Images are still stored as base64 in localStorage/export JSON. To keep files small, prefer URL references to hosted images and remove old base64 blobs before committing to the data files.
