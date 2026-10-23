# Pocket Money — how to use it

It's a web app: just open the link. It works offline too.

## For the family

1. Open the app link on your phone.
2. Enter your starting numbers and tap **Start**.

**Sync across family phones:** Settings → Family sync → **Sign in with Google**. Everyone signs in with the **same Gmail**. In Settings → "This phone is", type `Papa`, `Mummy` etc. so you can see who added what.

**Backup:** Settings → Backup → Export, every few weeks.

## How the maths works

- On the 1st of every month, the **base allowance** (₹1,000) goes into the main account.
- Leftover = base − what was spent that month (never below ₹0). Money from relatives doesn't count.
- Next month, **leftover × multiplier** (2×) is added as a bonus, straight into the savings jar.
- Example: spend ₹700 in November → ₹300 left → on 1 December: main = ₹300 + ₹1,000 = **₹1,300**, jar = **₹600**.

---

## For whoever hosts it (one-time)

### Files

`index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`. Upload all of them together to any static host (GitHub Pages, Netlify, Vercel). It must be served over **https** for offline to work.

When you change `index.html`, also change `VERSION` in `sw.js` (e.g. `pm-v2`) so phones get the new version.

### Turning on Google sign-in + sync (free Firebase plan)

Do this once, and every family using the link gets sync.

1. **console.firebase.google.com** → Add project.
2. **Authentication → Get started → Sign-in method → Google → Enable.**
3. Authentication → **Settings → Authorized domains** → add the app's domain (e.g. `yourname.github.io`).
4. **Firestore Database → Create database** → location `asia-south1 (Mumbai)` → Production mode.
5. **Rules** tab → replace everything with this → Publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    match /families/{uid}/{doc=**} {
      allow read, write: if request.auth.uid == uid;
    }
  }
}
```

6. **Project settings ⚙️ → Your apps → Web `</>`** → copy the `firebaseConfig = { ... }` values.
7. In `index.html`, replace `const FIREBASE_CONFIG = null;` with `const FIREBASE_CONFIG = { ...the values... };` and upload it again.

Each family's data is private to its own Gmail account (the rules above enforce that), so any number of families can share the same link.
