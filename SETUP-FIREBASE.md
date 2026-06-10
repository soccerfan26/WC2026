# Firebase setup — one-time, ~10 minutes

This connects the prediction pool (accounts + saved brackets + leaderboard) to your site.
Do this BEFORE the first match (June 11, 2:00 PM CT) so people can submit picks.

## 1. Create the project
1. Go to https://console.firebase.google.com and sign in with any Google account
2. Click **Create a project** (or "Add project"), name it `worldcup2026`
3. Turn OFF Google Analytics when asked (not needed) → Create

## 2. Turn on email/password accounts
1. In the left sidebar: **Build → Authentication** → Get started
2. Under "Sign-in method", click **Email/Password** → Enable → Save

## 3. Create the database
1. Left sidebar: **Build → Firestore Database** → Create database
2. Choose **Start in production mode** → pick the default US location → Enable

## 4. Paste in the security rules (this enforces the kickoff lock)
1. In Firestore, open the **Rules** tab
2. Delete what's there, paste the entire contents of `firestore.rules` from this folder
3. Click **Publish**

## 5. Connect your website
1. Click the gear icon (top left) → **Project settings**
2. Scroll to "Your apps" → click the **</>** (Web) icon
3. Nickname: `worldcup-site` → Register app (skip hosting)
4. You'll see a code block with `const firebaseConfig = { apiKey: "...", ... }`
5. Copy just the values into `firebase-config.js` in this folder, replacing the PASTE placeholders

## 6. Authorize your site's address
1. Authentication → **Settings** tab → **Authorized domains**
2. Make sure `jmeneley.github.io` is in the list (click Add domain if not)

## 7. Publish
Commit and push this repo. Done — the "My Picks" and "Leaderboard" tabs go live on the site.

## Notes
- The config values in firebase-config.js are safe to publish publicly; access control comes from the rules.
- The lock (no edits after June 11, 19:00 UTC) is enforced by the server rules — users can't bypass it.
- Free tier limits are far beyond what a friends-and-family pool will use.
- To remove a troll account: Authentication → Users → delete; their picks doc can be deleted in Firestore → Data → picks.
