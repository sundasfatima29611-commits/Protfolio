# Sundas Fatima — Portfolio

One self-contained file: `index.html` (photo, VitalFit screens, Florabloom video,
logo and CV are all embedded — works offline, no extra files needed).

============================================================
DEPLOY TO YOUR TWO ADDRESSES
============================================================

I can't log in to your Netlify or GitHub accounts, so you do these final
clicks — each takes about a minute. The file is ready to go as-is.

------------------------------------------------------------
A)  Netlify  ->  https://sundasprotfolio.netlify.app/
------------------------------------------------------------
Easiest (drag & drop):
1. Sign in at https://app.netlify.com
2. If the site "sundasprotfolio" doesn't exist yet:
   - Click "Add new site" -> "Deploy manually".
   - Drag `index.html` (or the ZIP) onto the upload box.
   - Then Site settings -> Change site name -> type `sundasprotfolio`.
3. If the site already exists:
   - Open it -> "Deploys" tab -> drag `index.html` onto
     "Drag and drop your site output folder here".
Your site goes live at https://sundasprotfolio.netlify.app/

------------------------------------------------------------
B)  GitHub Pages  ->  https://sundasfatima29611-commits.github.io/Protfolio/
------------------------------------------------------------
1. Sign in at https://github.com (account: sundasfatima29611-commits)
2. Create a repository named exactly:  Protfolio  (Public)
3. In the repo: "Add file" -> "Upload files" -> drag `index.html` ->
   "Commit changes".
4. Settings -> Pages -> Build and deployment:
   Source = "Deploy from a branch", Branch = main, Folder = / (root) -> Save.
5. Wait ~1 minute. Your site appears at:
   https://sundasfatima29611-commits.github.io/Protfolio/

> Tip: GitHub Pages needs the file named `index.html` (it is) so it loads
> automatically at the repo URL.

------------------------------------------------------------
Optional: push code from VS Code (GitHub)
------------------------------------------------------------
If you prefer Git instead of drag-and-drop, from your project folder:
   git init
   git add index.html README.md
   git commit -m "Portfolio site"
   git branch -M main
   git remote add origin https://github.com/sundasfatima29611-commits/Protfolio.git
   git push -u origin main
Then enable Pages as in step 4 above.

============================================================
EDIT LATER
============================================================
Everything is inside index.html. To change text, just edit the words.
Your email/phone: search the file for  sundasfatima29611@gmail.com
Accent color: top of the file in :root  (--accent is the coral).
