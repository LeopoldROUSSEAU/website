# My Site (Jekyll, for GitHub Pages)

A small, plain, static site. GitHub Pages builds it for you automatically —
there's no Node, no npm, no separate build step, and nothing to run locally
unless you want a local preview.

## Setting up a brand-new repo from scratch

To avoid any leftover state from a previous attempt, start with a **new,
empty** GitHub repository rather than reusing an old one.

1. On GitHub, click **New repository**. If you want this to be your main
   user site (served at `https://USERNAME.github.io/` directly, no
   subpath), name it exactly `USERNAME.github.io` — replacing `USERNAME`
   with your actual GitHub username. Otherwise, any name works and the
   site will be served at `https://USERNAME.github.io/repo-name/`.
2. Leave it empty — don't add a README, license, or .gitignore on GitHub's
   side, since this folder already has those.
3. On your computer, unzip this project, open a terminal/PowerShell
   **inside the unzipped folder**, and run:

   ```
   git init
   git add -A
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/USERNAME/REPO-NAME.git
   git push -u origin main
   ```

   Replace `USERNAME/REPO-NAME.git` with the actual repo URL — you can
   copy it from the green "Code" button on the new repo's GitHub page.
4. On GitHub, go to **Settings → Pages**. Set Source to **"Deploy from a
   branch"**, branch **main**, folder **/ (root)**, and Save.
5. If you named the repo `USERNAME.github.io`, leave `baseurl: ""` in
   `_config.yml` as-is. If you used a different repo name, open
   `_config.yml` and set `baseurl: "/REPO-NAME"`.
6. Wait a minute, then check the Actions tab for a "pages build and
   deployment" run, and visit the URL shown on the Pages settings page.

Since this is a fresh repo with no history, there's nothing left over to
conflict with — no old workflow files, no duplicate configs, no stray
folders.


