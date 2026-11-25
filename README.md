# KitaGames

A fully static browser-game site with 27 activities, real cover artwork, fullscreen play, Google/email/guest sign-in, and private cloud saves through Firebase Authentication + Cloud Firestore.

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

- `RULES.txt` — full instructions and rules for all 27 games/activities.
- `NEON_DISTRICT_RULES.txt` — detailed controls, jobs, vehicles and wanted-level guide for Neon District.
- `FIREBASE_SETUP.txt` — click-by-click Firebase and GitHub Pages setup.
- `FIRESTORE_RULES.txt` — complete Firestore Security Rules to paste into Firebase.
- `COMMUNITY_GAME_RULES.txt` — account limits, upload format, safety and publishing rules for player-made games.
- `FIRESTORE_INDEXES.txt` — explains why the latest public library needs no custom index.

## Technical notes

- Static HTML, CSS and JavaScript. No build step, terminal, npm or server required.
- Firebase modular Web SDK is loaded from Google's CDN (version 13.4.0).
- No Firebase Admin credentials are included. The browser config is public by design; Firestore authorization is enforced by Security Rules.
- Game artwork is bundled locally in `assets/`, so the covers do not depend on third-party image hosts.
- Guest saves remain tied to the anonymous Firebase account. The site supports linking a guest account to Google so the same UID/profile can be retained.


## Community games (player uploads)

KitaGames includes a community creator. A user signed in with Google or email
can paste a self-contained HTML game or upload one `.html` file, preview it in
a sandbox, and save it directly to Cloud Firestore. Users can have up to three
game documents in fixed reusable slots; this is enforced by Firestore Rules.
Guest accounts can play but cannot publish. Games can be private drafts or
publicly published.

No custom backend, Firebase Storage, Cloud Functions, or command-line tooling
is required. Game source is stored in Firestore, limited to 80,000 characters,
and played inside an isolated iframe with a restrictive Content Security
Policy. Publish the updated `FIRESTORE_RULES.txt` in the Firebase Console
before using the community creator.

See `FIREBASE_SETUP.txt` for no-command Firebase setup, `COMMUNITY_GAME_RULES.txt` for uploader rules, and `FIRESTORE_INDEXES.txt` for the index-free community query design. Firestore usage is still subject to Google Firebase quotas and pricing for reads, writes, stored data and network transfer; a no-server design does not mean unlimited or necessarily free usage.


## Community publishing and share links

Published player games are stored in Firestore and loaded from the top-level
`communityGames` collection query on every page load. A Firestore realtime
listener also keeps the public shelf updated while the site is open. Each
published game has a Share action that copies a direct GitHub Pages URL such as
`https://YOUR-USERNAME.github.io/kitagames/?play=FIREBASE_UID/game-1`.
Opening or refreshing that URL fetches the published game directly from
Firestore and launches it. Private drafts are not publicly readable. The three
fixed game slots and public read restrictions are enforced by the rules in
`FIRESTORE_RULES.txt`.


## Neon District: Open City

An original top-down open-city sandbox is included as a built-in game. Explore
the city on foot or in a driveable car, take delivery jobs, find cash stashes,
visit the garage, and try to lose the police when your wanted level rises. It
uses Canvas 2D and procedural art, runs entirely in the browser, and supports
keyboard controls plus touch controls on phones. Progress cash and completed
jobs are stored locally in the browser.

## Community games — no custom collection-group index

This release moves player-created games to a top-level Firestore collection
`/communityGames/{uid}__game-1` through `__game-3`. The public shelf uses a
regular collection query, so the collection-group index warning is removed.
The three fixed document IDs still enforce the three-game-per-account limit
in Firestore Security Rules. Existing nested creator documents are migrated
when their owner signs in after the updated rules are published. Publish the
new `FIRESTORE_RULES.txt` before using this release.
