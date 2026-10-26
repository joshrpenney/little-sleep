# Little Sleep — Baby Sleep Tracker

A mobile-friendly first version of a baby sleep tracker designed to host on GitHub Pages. It supports:

- Start/stop a sleep session, with a live duration timer
- Keeps an active session's start time if you close and reopen the site
- Today's total sleep and session count
- A user-editable preferred morning start, bedtime, and wake-window range
- A suggested next sleep window based on the last completed sleep and the chosen wake window
- Live syncing between two phones through Firebase Firestore
- Email/password sign-in; there is no public sign-up form in the app

## Setup overview

### 1. Create a Firebase project

1. Go to https://console.firebase.google.com/ and create a project.
2. In **Authentication → Sign-in method**, enable **Email/Password**.
3. In **Authentication → Users**, manually add one account for each parent. The app intentionally does not provide public registration.
4. In **Firestore Database**, create a database.
5. In **Project settings → General → Your apps**, register a Web app and copy its Firebase config.

### 2. Configure the files

1. Edit `firebase-config.js` and replace the placeholder Firebase values with the values from your Firebase web app config.
2. Replace `FAMILY_SPACE_ID` with the same long, random string on both phones. Do not use a guessable value such as `baby` or your child's name.
3. In Firebase **Firestore Database → Rules**, paste the contents of `firestore.rules` and publish.

**Security note:** The included rules are a minimal starter. They allow any authenticated account in this Firebase project to access the shared family data. Because you manually create the only two accounts and do not add public sign-up, that may be acceptable for a private prototype. Before adding any other accounts or expanding the app, change the rules to check family membership per user. Never publish passwords or service-account keys. Firebase web configuration is not a server secret; the security rules are what protect the data.

### 3. Put it on GitHub

1. Create a new GitHub repository (for example, `little-sleep`).
2. Upload `index.html`, `firebase-config.js`, and `firestore.rules` to the repository root.
3. Go to **Settings → Pages**. Choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Wait for GitHub Pages to publish the site. Open the published HTTPS URL on both phones and sign in with the two accounts.
5. Add the site to each phone's home screen from the browser menu for an app-like shortcut.

## Notes / limitations in this first version

- Both phones need an internet connection for changes to sync. Firebase sends live updates to both devices.
- If a session is active and the page is closed, its start timestamp remains stored and the duration resumes correctly when reopened.
- This first version allows one active sleep session at a time across both phones, which helps prevent duplicate timers.
- The next-sleep recommendation is a configurable planning estimate, not medical advice or a rigid schedule. Follow baby's cues and guidance from your health visitor/clinician.
- It stores sleep times only; feeds, nappies, notes, charts, and push notifications can be added in later versions.
