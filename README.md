# Buwaya Tracker

A static website (Home page with news + dynasty graph) and a C console program that share the same data file. All sample names, links and news are fictional.

```
index.html              the website (no build step)
buwaya_tracker.c        the C program (reads data/politicians.txt)
data/
  politicians.txt       id|name|party|position|platform|track_record
  relations.txt         id|id|type          (spouse, parent, sibling, cousin)
  news.txt              date|category|title|summary|link|politician id
```

## Editing the data on GitHub (no coding)

1. Open a file in the `data` folder on GitHub.
2. Click the **pencil icon** (Edit this file).
3. Add or change lines, then click **Commit changes**.
4. The site updates within a minute or two.

Rules for all three files:
- One record per line, fields separated by `|`. Never type `|` inside a field.
- Lines starting with `#` are comments and are ignored.
- **politicians.txt**: IDs must be unique numbers. New parties get a color automatically. Field limits (for the C program): name 100, party and position 50, platform and track record 300 characters.
- **relations.txt**: use the politician IDs. For `parent`, the first ID is the parent, the second is the child. Dynasties are worked out automatically from connected relatives.
- **news.txt**: date as `YYYY-MM-DD`. The link and politician ID are optional (`...|summary||4` adds a profile link but no article link). Only `http` and `https` links are shown.

## Publish with GitHub Pages

1. Create a repository and upload everything in this folder (keep the `data` folder).
2. Go to **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
3. Open `index.html` and replace `YOUR-USERNAME/YOUR-REPO` in the `EDIT_URL` line near the top of the script, so the "Edit on GitHub" links point to your repository.

Your site will be at `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

## Preview on your computer

Browsers block data loading when you double-click `index.html`. Run a small local server in this folder instead:

```
python -m http.server 8000
```

Then open http://localhost:8000.

## C program

Run it from this folder so it finds `data/politicians.txt`:

```
gcc -Wall -Wextra -o buwaya_tracker buwaya_tracker.c
./buwaya_tracker
```

The C program rewrites `data/politicians.txt` when you choose Exit, so comment lines are not allowed in that one file. Keep notes in the other two files instead.
