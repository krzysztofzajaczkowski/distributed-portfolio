
[![LinkedIn][linkedin-shield-zajaczkowski]][linkedin-url-zajaczkowski] [![Build and deploy][build-passing-shield]][build-passing-url] 

# Distributed Portfolio

## Table of Contents

* [About the Project](#about-the-project)
  * [Built With](#built-with)
* [Adding new project](#adding-new-project)
	* [Index file template](#index-file-template)
* [Custom GitHub Actions](#custom-github-actions)

## About the project
This project was made as part of my experiments with PowerShell and GitHub Actions. *Design of this web application doesn't belong to me*. During deployment, my public repositories are scanned for `.portfolio` directory with `cover-image.png` and `index.mdx` files. These files are downloaded to Gatsby `projects` directory and after that application is built and deployed to GitHub Pages. Thanks to that, information about projects doesn't have to be centralized inside this repository and can be distributed among all repositories.

### Built with
* Gatsby
* PowerShell (for custom GitHub Actions)

## Adding new project
Adding new project to this portfolio requires project's repository to be public (so it's publicly accessible through GitHub API). Apart from that prerequisite, there are 2 steps for introducing project to the portfolio:

1. Add `.portfolio` directory with files `cover-image.png` and `index.mdx` based on [template](#index-file-template).
2. Add workflow that uses [File change trigger](https://github.com/krzysztofzajaczkowski/file-change-trigger)  GitHub Action to trigger portfolio's redeployment.

### Index file template
```
---
title: "<PROJECT_TITLE>"
category: "<PROJECT_CATEGORY>"
emoji: "<EMOJI>"
screenshot: "./cover-image.png"
github: "<REPOSITORY_URL>"
external: ""
tags:
  - TAG_1
  - TAG_2
visible: true
position: 1
---

<PROJECT_DESCRIPTION>
```

## Custom GitHub Actions
Custom GitHub Actions that I've built specifically for this project:
* [File change trigger](https://github.com/krzysztofzajaczkowski/file-change-trigger) - this action uses GitHub API to trigger specified workflow using `workflow_dispatch` event if any change was made in path that is observed. Thanks to this action, any changes to repository's `.portfolio` directory trigger portfolio redeployment.
* [Repository template downloader](https://github.com/krzysztofzajaczkowski/repo-template-downloader) - this action uses GitHub API to list all user's repositories, look for `.portfolio` directory in each of them and download it to specified path if it exists. Thanks to this action, all projects descriptions are downloaded and included in Gatsby application during redeployment.


[linkedin-shield-zajaczkowski]: https://img.shields.io/badge/LinkedIn-Zajączkowski-blue?logo=linkedin
[linkedin-url-zajaczkowski]: https://www.linkedin.com/in/krzysztof-m-zajaczkowski/
[build-passing-shield]: https://img.shields.io/github/workflow/status/krzysztofzajaczkowski/distributed-portfolio/Build%20and%20deploy?label=Build%20and%20deploy&logo=GitHub
[build-passing-url]: https://github.com/krzysztofzajaczkowski/distributed-portfolio/actions/workflows/action.yml