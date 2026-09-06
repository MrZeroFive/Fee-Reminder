# Fee Reminder — installable app files

Your `Fee-Reminder` repo was missing the files a browser needs to offer
"Install app". This package adds them, using a custom bell + fee icon,
and gives Fee Reminder its own unique app identity (separate from PPS
Tools) so Chrome won't confuse the two.

## 📁 What's in this folder

```
manifest.json     app name, colors, and icon list — unique id "/Fee-Reminder/"
sw.js             minimal service worker (required for "Install app")
favicon.ico       browser-tab icon
icons/            the bell+fee icon resized 16px–512px, plus the original
```

## 🚀 How to add these to your existing Fee-Reminder repo

1. Go to `github.com/mrzerofive/Fee-Reminder`.
2. Upload **all files from this folder** into the repo root, keeping the
   `icons/` folder structure (drag-and-drop the whole folder works on
   github.com, or use `git add . && git commit && git push`).
3. Open your existing `index.html` in the repo (click the file → pencil/edit
   icon) and add these lines inside the `<head>...</head>` section
   (anywhere near the top, next to your existing `<meta>` tags):

   ```html
   <meta name="theme-color" content="#0b3d62">
   <link rel="manifest" href="./manifest.json">
   <link rel="icon" type="image/png" sizes="32x32" href="./icons/icon-32.png">
   <link rel="icon" type="image/png" sizes="16x16" href="./icons/icon-16.png">
   <link rel="icon" type="image/png" sizes="192x192" href="./icons/icon-192.png">
   <link rel="shortcut icon" href="./favicon.ico">
   <link rel="apple-touch-icon" sizes="180x180" href="./icons/icon-180.png">
   ```

4. Still in `index.html`, add this just before the closing `</body>` tag
   (last line of the file, or right before `</html>` if there's no
   separate `</body>`):

   ```html
   <script>
   if ("serviceWorker" in navigator) {
     window.addEventListener("load", function () {
       navigator.serviceWorker.register("./sw.js").catch(function () {});
     });
   }
   </script>
   ```

5. Commit the changes.

## 📲 Before you install it again

Your phone likely still has an old "Fee-Reminder" shortcut from before
(the one that caused "already installed"). Remove it first:

- Long-press the old **Fee-Reminder** icon on your home screen / app
  drawer → **Uninstall** / **Remove**.

Then also clear the site's old data so Chrome forgets the broken state:

- Chrome → **⋮ → Settings → Site settings → All sites** → search
  `mrzerofive.github.io` → open the `Fee-Reminder` entry (if separate) →
  **Clear & reset**.

## ✅ Then install fresh

1. Open `https://mrzerofive.github.io/Fee-Reminder/` in Chrome.
2. **⋮ menu → Install app** (or the install icon in the address bar).
3. You should now see the new bell+fee icon, and it will install as its
   own separate app from PPS Tools.

## 🔁 Same approach for future apps

Every new project needs its **own** `manifest.json` with:
- a unique `"id"` (e.g. `"/RepoName/"`)
- a unique `"name"`
- its own `icons/` set

That's what keeps Chrome from mixing up separate apps hosted under the
same `mrzerofive.github.io` account.
