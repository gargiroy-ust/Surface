**Surface** is a project demonstrating how to use and manage **Git submodules**.  
It includes another GitHub repository — [submarines](https://github.com/your-username/submarines) — as a submodule to 
highlight modular and reusable code design.
You want to be able to treat the two projects as separate yet still be able to use one from within the other.

## Project Structure
```
surface/
├── submarines/ # Git submodule (external repo)
├── .gitmodules # Tracks submodule path and URL
├── main.py
└── README.md
```

## What is a Git Submodule?

A Git submodule is a way to include another Git repository within your own project as a dependency. This is useful for:
- Reusing shared libraries or components across multiple projects.
- Keeping separate version histories for modular parts.
- Avoiding copy-pasting code between projects.

## Adding a Submodule 
bash

git submodule add https://github.com/your-username/submarines.git submarines
This creates a .gitmodules file that tracks submodule settings.

-Sample .gitmodules file
[submodule "submarines"]
    path = submarines
    url = https://github.com/your-username/submarines.git
    branch = main
Optional: Add branch = main manually if you want git submodule update --remote to fetch from main.

##  How to Clone This Project with Submodules

in git bash run the below command:
git clone --recurse-submodules https://github.com/your-username/surface.git

If you've already cloned it without the --recurse-submodules flag, then follow these steps:
cd surface
git submodule update --init --recursive

## Pulling in Upstream Changes from the Submodule Remote

When you add a submodule, it tracks a specific commit, not a branch.
So even if the submodule repo is updated (new commits), your project won’t see them unless you update it manually.

bash
git submodule update --remote

Tells Git to:

1. Go into each submodule
2. Fetch from its remote origin
3. Checkout the latest commit on the configured branch (e.g., main)
Then, in your parent repo, you’ll see that the submodule pointer has moved to this newer commit.

bash
git add .
git commit -m "Update submarines submodule to latest commit"
git push

- Configuration
You can configure which branch a submodule tracks:

- Inside your submodule folder
git checkout main

- Back in root repo
git config -f .gitmodules submodule.submarines.branch main
This makes --remote always fetch from the main branch of the submarines submodule.











