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

* 14.1.4 : OK
* 14.2.0-canary.27: OK
* 14.2.0-canary.28: BROKEN
* 14.2.0 : BROKEN
* 14.2.1 : BROKEN
* 14.2.2 : BROKEN
* 14.3.0-canary.11: BROKEN

Apparently the issue has been introduced in https://github.com/vercel/next.js/releases/tag/v14.2.0-canary.28

I would bet that the issue was introduced in this PR : https://github.com/vercel/next.js/pull/63157
