# KitaGames

A fully static browser-game site with 26 activities, real cover artwork, fullscreen play, Google/email/guest sign-in, and private cloud saves through Firebase Authentication + Cloud Firestore.

## What is included

- 20 arcade, puzzle, memory, strategy and skill games.
- 6 relaxed activities: Cloud Drift, Tiny Garden, Koi Pond, Rainy Window, Stargazer and Color Studio. These are intentionally non-competitive: no clocks, scores or leaderboards.
- 20 bundled WebP cover illustrations in `assets/`.
- Responsive game library, search, categories and favorites.
- Fullscreen game area (button or `F` key; `Escape` exits native fullscreen).
- Firebase sign-in: Google, email/password and anonymous guest.
- Firestore profile sync for favorites, personal bests and games played.
- Local storage fallback when a visitor has not signed in or Firebase is unavailable.
- Plain-text rules and setup documents.

## Publish on GitHub Pages — no commands

1. Extract `KitaGames-GitHub-Pages.zip` on your computer.
2. Create a GitHub repository (for example, `kitagames`).
3. In the repository, choose **Add file → Upload files**.
4. Upload **all** contents of the extracted folder, including the `assets` folder. Keep `index.html`, `.nojekyll`, the text files and `assets/` together at the repository root.
5. Commit the files to the `main` branch.
6. Open **Settings → Pages**. Select **Deploy from a branch**, branch `main`, folder `/(root)`, then Save.

## Enable Firebase login and cloud saving

The supplied Firebase web configuration is already in `index.html`. The Firebase console still needs Authentication providers and a Firestore database enabled. Follow `FIREBASE_SETUP.txt` in order, then publish the rules from `FIRESTORE_RULES.txt`.

Enable these Firebase Authentication providers:

- Google
- Email/Password
- Anonymous (for guest access)

Add your GitHub Pages host (for example `yourname.github.io`) to Authentication → Settings → Authorized domains. Create a Firestore database and publish the included rules. Do not use open/public Firestore rules.

## Text guides

- `RULES.txt` — full instructions and rules for all 26 games/activities.
- `FIREBASE_SETUP.txt` — click-by-click Firebase and GitHub Pages setup.
- `FIRESTORE_RULES.txt` — complete Firestore Security Rules to paste into Firebase.

## Technical notes

- Static HTML, CSS and JavaScript. No build step, terminal, npm or server required.
- Firebase modular Web SDK is loaded from Google's CDN (version 13.4.0).
- No Firebase Admin credentials are included. The browser config is public by design; Firestore authorization is enforced by Security Rules.
- Game artwork is bundled locally in `assets/`, so the covers do not depend on third-party image hosts.
- Guest saves remain tied to the anonymous Firebase account. The site supports linking a guest account to Google so the same UID/profile can be retained.
