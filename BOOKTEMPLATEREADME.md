# Book Template
This is a repository with the basic files/structure for a Tech Outreach lesson or set of lessons. It contains the setup to build a GitBook from the repository using GitHub actions.

## Files
Here is a breakdown of the files in this repository:

- [**.github/workflows/BuildGitBook.yml**](.github/workflows/BuildGitBook.yml): This file describes the GitHub action to build the GitBook from this repository. It places the code in a branch named `gh-pages`, which GitHub Pages can use to render the book online.
- [**styles/website.css**](styles/website.css): This file adds custom styles to the GitBook.
- [**.gitignore**](.gitignore): This file lists files that should be ignored by Git.
- [**book.json**](book.json): This file contains configuration information for the GitBook.
- [**BOOKTEMPLATEREADME.md**](BOOKTEMPLATEREADME.md): This is this file. It contains information about the book template.
- [**FollowAlong.md**](FollowAlong.md): This is an example file that will become a page of the published GitBook.
- [**PptTemplate.pptx**](PptTemplate.pptx): This is a PowerPoint file that contains our current theme.
- [**README.md**](README.md): This file is the landing page for the repository. It will not be published on the GitBook, and is designed for internal instructor reference only.
- [**StudentDesc.md**](StudentDesc.md): This file will be the landing page of the GitBook when it is published.
- [**SUMMARY.md**](SUMMARY.md): This file outlines the pages to be published on the GitBook.

## Getting Started
To use this template, follow these instructions:

1. Click the green "Use this template" button when viewing this repository on GitHub
1. Fill out a Repository name and Description
1. Click the green "Create repository from template" button
1. On the new repository, wait for the GitHub action to complete
    - This action will create the `gh-pages` branch
1. When the action is done, click on "Settings"
1. On the "Settings" page, on the left, click on "Pages"
1. In the "Build and deployment" section, click the dropdown under "Branch"
1. Select `gh-pages` as the branch
1. Click the "Save" button
1. Wait for a little while, and then refresh the "Pages" page
1. Click the link to the deployment - the GitBook should be published!

After the GitBook is up, all that's left is to actually create the lesson plan(s) in the repository. This file can be removed.
