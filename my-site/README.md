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

## Fixing the 404 you hit

GitHub Pages usually serves a repository at:

```
https://USERNAME.github.io/REPO-NAME/
```

— note the `/REPO-NAME/` on the end. If a site's links are written as
root-absolute paths like `/about`, they resolve to
`https://USERNAME.github.io/about`, which doesn't exist — hence "There
isn't a GitHub Pages site here."

This project avoids that by writing every internal link as
`{{ '/about/' | relative_url }}` instead of `/about/`. The `relative_url`
filter automatically prepends the correct subpath, using the `baseurl`
value in `_config.yml`.

**You need to set that value once**, in `_config.yml`:

- If your Pages URL is `https://USERNAME.github.io/REPO-NAME/`, set
  `baseurl: "/REPO-NAME"`.
- If your Pages URL is `https://USERNAME.github.io/` directly (only
  possible if the repo is literally named `USERNAME.github.io`), leave
  `baseurl: ""`.

## Publishing

1. Push this project to a GitHub repository (any name, public or private
   — Pages works with either on a paid plan; public repos get it for
   free).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a
   branch", and pick your main branch with the `/ (root)` folder.
4. Save. GitHub will build the site with Jekyll and publish it — usually
   within a minute or two. The Pages settings page shows the live URL
   once it's ready.

Every push after that rebuilds and republishes automatically.

## How pages work

Every `.md` file becomes a page, at a URL that mirrors its file path:

| File                       | URL                  |
|-----------------------------|----------------------|
| `index.md`                  | `/`                  |
| `about.md`                  | `/about/`            |
| `notes/index.md`            | `/notes/`            |
| `notes/first-note.md`       | `/notes/first-note/` |

A folder's `index.md` becomes that folder's own page. Nest folders as deep
as you like.

**One gotcha:** for an `index.md` inside a subfolder (like `notes/index.md`),
add an explicit `permalink` in its front matter pointing at the folder:

```markdown
---
title: "Notes"
permalink: /notes/
---
```

Without it, Jekyll's automatic "pretty" URL logic can turn it into
`/notes/index/` instead of `/notes/` — a page that exists, just not at the
URL anything links to. Flat files like `about.md` don't need this, only
`index.md` files inside folders.

**There is no automatic navigation menu.** Pages link to each other because
you write the links, inside the Markdown, using the `relative_url` pattern
shown above. `index.md` is set up as a hand-curated table of contents —
treat it as your site's front door, and edit it as your pages change.

## Adding a page

Create a new `.md` file. Start it with a small metadata block, then write
the page in Markdown:

```markdown
---
title: "Page Title"
---

Your content here. Link to other pages like this:
[About]({{ '/about/' | relative_url }})
```

To edit a page, edit its file. To remove one, delete its file (and any
links pointing to it).

## Changing the design

Everything visual is in `assets/css/style.css`. The top of the file is a
small set of variables:

```css
:root {
  --color-bg: #ffffff;
  --color-text: #111111;
  --color-link: #0000ee;
  --font-body: Georgia, 'Times New Roman', Times, serif;
}
```

The shared header/footer markup is in `_layouts/default.html` — edit it
once and every page updates.

## Changing the site name

Edit `title` and `description` at the top of `_config.yml`.

## Previewing locally (optional)

Not required — you can just push and check the live site. If you do want
a local preview, it needs Ruby and Jekyll installed:

```bash
gem install bundler jekyll
bundle init
bundle add jekyll
bundle exec jekyll serve
```

Then open `http://localhost:4000`.
