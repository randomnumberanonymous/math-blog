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
`git add .`

### 2. Commit the changes with a clear description of what you updated
`git commit -m "Add notes on Hartshorne Chapter 1 local properties"`


## Step 4: Push to GitHub

Ship your local changes up to your remote repository using your configured SSH channel:
Bash

`git push origin main`

### What Happens Automatically Next 🤖

The moment that git push finishes executing in your terminal, the rest of the pipeline happens completely in the cloud:

    - *Trigger:* GitHub detects a new push on the main branch and automatically wakes up your Quarto Publish GitHub Actions runner.

    - *Compile:* The cloud runner downloads your project, runs the Quarto engine to compile your .qmd files into optimized HTML/CSS, and handles all the math typesetting.

    - *Deploy:* The runner automatically commits those generated HTML files directly onto your remote gh-pages branch.

    - *Go Live:* GitHub Pages updates its web servers.

Within 1 to 2 minutes of running your git push origin main command, you can simply refresh https://randomnumberanonymous.github.io/ and your updates will be live for the world to see!
# The Web-to-Local Workflow
## Step 1: Edit on GitHub.com

    1. Go to your repository on GitHub.

    2. Click on any file (like hartshorne.qmd) and click the pencil icon (Edit this file).

    3. Make your edits right in the browser, scroll down, and click Commit changes... directly to the main branch.

    *Result:* The GitHub Actions runner instantly wakes up, compiles your changes, and updates your live website automatically.

## Step 2: Sync Your Fedora Machine (Crucial)

Because you made those changes directly on the cloud servers, your local computer doesn't know about them yet. Before you do any new work on your laptop, you must pull those changes down.

Open your Fedora terminal and run:
Bash

`cd ~/git/math-blog`

`git checkout main`

`git pull origin main`
