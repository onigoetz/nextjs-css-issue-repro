# CSS Issue repro

This issue was introduced in Next.js 14.2.0

The issue is that stylesheets from separate layouts get merged together if they have a CSS file in common.

* https://nextjs-css-issue-repro.vercel.app/
  * Loads `src/style.css` (green background)
* https://nextjs-css-issue-repro.vercel.app/leakingstyle
  * Loads `src/style.css` (green background)
  * Loads `src/app/(leakingstyle)/style.css` (red background)
* https://nextjs-css-issue-repro.vercel.app/otherstyle
  * Loads `src/app/(leakingstyle)/style.css` (blue background)

If you open the URL, you can see that the homepage ( https://nextjs-css-issue-repro.vercel.app/ ) has a *red* background even though it does not include the style for a red background.

More importantly, those two files have *no layout in common* they just happen to import the same stylesheet

This worked before Next 14.2.0
