# randomnumberanonymous.github.io
math etc related stuff

# Local workflow

## Step 1: Open Your Workspace

Navigate to your repository on your Fedora machine and open your text editor (like Neovim/Vim) to make your edits:
Bash

`cd ~/git/math-blog`

(Make your changes to your .qmd files, such as updating your algebraic geometry notes or fixing a proof layout).
## Step 2: Preview Locally (Optional but Recommended)

Before pushing to the live internet, you can render and preview the site locally to make sure your LaTeX equations render exactly how you want them to:
Bash

`quarto preview`

This will spin up a local development server and open a tab in your browser (usually at http://localhost:3213). It live-reloads as you save your files! Press Ctrl+C in your terminal when you're done.
## Step 3: Stage and Commit Your Changes

Once you are happy with your edits, take a snapshot of your work:
Bash

### 1. Stage all changes (.qmd files, configurations, images)
git add .

### 2. Commit the changes with a clear description of what you updated
git commit -m "Add notes on Hartshorne Chapter 1 local properties"


## Step 4: Push to GitHub

Ship your local changes up to your remote repository using your configured SSH channel:
Bash

`git push origin main`

### What Happens Automatically Next 🤖

The moment that git push finishes executing in your terminal, the rest of the pipeline happens completely in the cloud:

    Trigger: GitHub detects a new push on the main branch and automatically wakes up your Quarto Publish GitHub Actions runner.

    Compile: The cloud runner downloads your project, runs the Quarto engine to compile your .qmd files into optimized HTML/CSS, and handles all the math typesetting.

    Deploy: The runner automatically commits those generated HTML files directly onto your remote gh-pages branch.

    Go Live: GitHub Pages updates its web servers.

Within 1 to 2 minutes of running your git push origin main command, you can simply refresh https://randomnumberanonymous.github.io/ and your updates will be live for the world to see!
