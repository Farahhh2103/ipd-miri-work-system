IPD Miri - Sistem Semakan Kerja (Autosync template)

This repository contains a ready-to-deploy static web app that syncs work records and photos in realtime using Firebase Firestore + Storage.

What I added for you:
- index.html (app UI + realtime sync code)
- firebase.json (hosting config)
- .firebaserc (placeholder for your Firebase project id)
- firestore.rules / storage.rules (recommended security rules - require auth)

Before deploying (required):
1) Create a Firebase project in the Firebase Console if you don't have one.
2) Get your Web SDK config (Firebase Console -> Project Settings -> Your apps -> Add web app) and replace the placeholder in index.html:
   const firebaseConfig = { apiKey: "REPLACE_ME", authDomain: "REPLACE_ME.firebaseapp.com", projectId: "REPLACE_ME", storageBucket: "REPLACE_ME.appspot.com", messagingSenderId: "REPLACE_ME", appId: "REPLACE_ME" };

3) (Recommended) Enable Anonymous Authentication in Firebase Console -> Authentication -> Sign-in method -> Anonymous -> Enable.

4) Update .firebaserc "default" to your Firebase project id (or run `firebase use --add` when using the CLI).

5) Set Firestore & Storage rules in the Console or using CLI. The provided rules (firestore.rules and storage.rules) require authentication (anonymous or other). If you want fully public rules (NOT recommended for production), you can change `if request.auth != null` to `if true` but be aware of security/storage abuse risk.

Deploy with Firebase Hosting (recommended):
- Install Firebase CLI: `npm install -g firebase-tools`
- Login: `firebase login`
- From this repository root (where firebase.json exists) run `firebase init` and choose Hosting; if asked for public directory you can keep `.` because the firebase.json is pre-configured.
- Finally deploy: `firebase deploy --only hosting`

After successful deploy the public link will be:
  https://<YOUR_FIREBASE_PROJECT_ID>.web.app
or
  https://<YOUR_FIREBASE_PROJECT_ID>.firebaseapp.com

Alternative (GitHub Pages):
- If you prefer GitHub Pages, push the repo and enable Pages in repo settings. Replace firebaseConfig in index.html as above. Note: GitHub Pages only hosts the static files; Firestore/Storage still require a Firebase project configured.

Security & notes:
- The app uses a single Firestore document (artifacts/{appId}/public/data/miri_work_records_v2). For scalability you can migrate to per-room documents to reduce contention.
- The app stores photos in browser IndexedDB for offline access and uploads to Firebase Storage (the Storage URL is saved to Firestore so other clients can fetch and cache it).
- Test with two browsers/devices concurrently to confirm realtime sync.

If you want, I can now:
- Help you replace the placeholders if you paste your Firebase config here (or provide it through a secure channel).
- Deploy on your behalf if you give me the Firebase project ID and grant me deploy access (not recommended to share secrets here).

Repository: https://github.com/Farahhh2103/ipd-miri-work-system
