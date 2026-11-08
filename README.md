# Al-Ammer School Game (managed by Yousef)

A real-time multiplayer word-guessing game. The owner of a room sets questions with 10 words each, players race to type the words in 15 seconds, and faster answers earn more points (100 → 10).

**Dependencies:** none to install. The site is one `index.html` that loads the Firebase SDK from a CDN. Firebase's free (Spark) plan is enough.

## 1. Create the Firebase backend (GitHub Pages is static, so Firebase gives the real-time part)

1. Go to https://console.firebase.google.com → **Add project** (name: `al-ammer-game`; Analytics not needed).
2. **Build → Realtime Database → Create database** → pick a region → start in *locked mode*.
3. **Build → Authentication → Get started**, then enable two providers under *Sign-in method*:
   - **Anonymous** (for players and room owners)
   - **Email/Password** (for the hidden admin panel)
4. **Authentication → Users → Add user**: create your admin email + a strong password. This is the only account that can open the hidden admin panel.
5. Open `database.rules.json`, replace both `ADMIN_EMAIL_HERE` with that admin email, then paste the whole file into **Realtime Database → Rules → Publish**.
6. **Project settings (gear) → General → Your apps → Web (`</>`)** → register an app → copy the `firebaseConfig` values.
7. Open `index.html`, find `const firebaseConfig`, and paste your values (`apiKey`, `authDomain`, `databaseURL`, `projectId`, `appId`).
   The `databaseURL` looks like `https://xxxx-default-rtdb.firebaseio.com`.

## 2. Publish on GitHub Pages

1. Create a GitHub repository (e.g. `al-ammer-game`), public.
2. Upload `index.html` (and optionally this README and the rules file) to the repository root.
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `(root)` → Save.**
4. After a minute your game is live at `https://YOUR-USERNAME.github.io/al-ammer-game/`.
5. Back in Firebase: **Authentication → Settings → Authorized domains → Add domain** → `YOUR-USERNAME.github.io`.

## 3. How to play

- **Owner:** open the site → type your name → *Create a room* (edit the questions if you like; format `Question | word1, word2, …`, use `/` for accepted alternatives) → share the 5-letter code or the invite link → press **Start game**. The owner panel lets you end a round, move on, reset, remove players or close the room. Keep the owner's tab open, because it checks the answers.
- **Players:** type a name, enter the room code, and type words before the timer ends.
- **Hidden admin panel:** click the *Al-Ammer School Game* title 5 times, press `Ctrl+Shift+A`, or add `#admin` to the URL, then sign in with the admin email. You can see all rooms, view their secret words, delete rooms and publish a site-wide announcement.

## Test locally (optional)

```
python -m http.server 8000
```
Then open http://localhost:8000
