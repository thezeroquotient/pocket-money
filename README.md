# Pocket Money

Track pocket money and grow a savings jar. Open the link, no sign-up: **https://thezeroquotient.github.io/pocket-money/**

## How to use it

1. Open the link on your phone.
2. Enter your starting numbers and tap **Start**.
3. Tap the black **+** to add spending or money you receive.

Your data stays on your phone. Now and then, go to Settings → **Save backup** and keep the file (send it to yourself on WhatsApp or save it to Drive). On a new phone, open the link and tap **Restore from a backup**.

## How the maths works

- On the 1st of every month, the **base allowance** (₹1,000) goes into the main account.
- Leftover = base − what was spent that month (never below ₹0). Money from relatives doesn't count.
- Next month, **leftover × multiplier** (2×) is added as a bonus, straight into the savings jar.
- Example: spend ₹700 in November → ₹300 left → on 1 December: main = ₹300 + ₹1,000 = **₹1,300**, jar = **₹600**.

The base and multiplier can be changed in Settings.

## For developers

Static files, no build step: `index.html`, `manifest.json`, `sw.js` and the icons. `sw.js` keeps the app working offline. When you change `index.html`, bump `VERSION` in `sw.js`.
