# Crunchy Hugo Theme

This repository contains a theme for [Hugo](https://gohugo.io/), based on the [DocDock](http://docdock.netlify.com/) Hugo theme.

# Installation

Check that your Hugo version is minimum `0.30` with `hugo version`. We assume that all changes to Hugo content and customizations are going to be tracked by git (GitHub, Bitbucket etc.). Develop locally, build on remote system.

## Step 1: Initialize Hugo

You can set up a new Hugo installation using:

```sh
hugo new site projectname
```

## Step 2: Install Crunchy Hugo Theme

There are a few ways to install the Crunchy Hugo Theme.

### Option 1: git clone

```sh
cd themes
git clone https://github.com/CrunchyData/crunchy-hugo-theme.git
```

### Option 2: Download

Download from https://github.com/CrunchyData/crunchy-hugo-theme and place the root folder in `themes`

### Option 3: git submodule

If you are working in a git project you can add the theme as a submodule:

## Step 3: Configuration

Use this as the basis for your `config.toml` file:

```toml
baseURL = ""
canonifyurls = true
defaultContentLanguage = "en"
defaultContentLanguageInSubdir= false
enableMissingTranslationPlaceholders = false
languageCode = "en-us"
publishDir = "../docs"
pygmentsCodeFences = true
pygmentsStyle = "monokailight"
relativeURLs = true
theme = "crunchy-hugo-theme"
title = "Your Project Name"

[params]
editURL = "https://github.com/CrunchyData/path/to/project"
showVisitedLinks = false # default is false
themeStyle = "original" # "original" or "flex" # default "flex"
themeVariant = "" # choose theme variant "green", "gold" , "gray", "blue" (default)
ordersectionsby = "weight" # ordersectionsby = "title"
disableHomeIcon = false # default is false
disableSearch = false # default is false
disableNavChevron = false # set true to hide next/prev chevron, default is false
highlightClientSide = false # set true to use highlight.pack.js instead of the default hugo chroma highlighter
menushortcutsnewtab = false # set true to open shortcuts links to a new tab/window
enableGitInfo = true

[outputs]
home = [ "HTML", "RSS", "JSON"]

# [[menu.shortcuts]]
# pre = "<h3>More</h3>"
# name = "<i class='fa fa-github'></i> <label>Github repo</label>"
# identifier = "ds"
# url = "https://github.com/CrunchyData/postgres-operator"
# weight = 10
#
# [[menu.shortcuts]]
# name = "<i class='fa fa-cloud-download'></i> <label>Download</label>"
# url = "https://github.com/CrunchyData/postgres-operator/releases/download/2.6/postgres-operator.2.6.tar.gz"
# weight = 11
#
# [[menu.shortcuts]]
# name = "<i class='fa fa-bookmark'></i> <label>Kubernetes Documentation</label>"
# identifier = "kubedoc"
# url = "https://kubernetes.io/docs/"
# weight = 20
#
# [[menu.shortcuts]]
# name = "<i class='fa fa-file'></i> <label>License</label>"
# url = "https://github.com/CrunchyData/postgres-operator/blob/master/LICENSE.md"
# weight = 22
```

# Testing

You can test your deployment by running the Hugo server module:

```sh
hugo server
```

By deafult, this will make the documentation available at http://localhost:1313 but be sure to read the output to where it binds.

# Deployment

You can build all the static docs by running:

```sh
hugo
```

By default, this outputs to a documentation directory above the project directory name `docs/`. You can configure this to what makes sense for your project.

# FAQ

## Supported File Types

By default, standalone Hugo supports HTML and Markdown formats (including Blackfriday and Mmark).

Using external helpers, you can use Asciidoc, reStructuredText, or pandoc using files with the associated extensions. Hugo will call external commands using the relevant helper to generate the content.

See more information regarding supported file types in Hugo [here](https://gohugo.io/content-management/formats/).

## Printing and PDFs

The CSS styles for this theme strip out unnecessary content such as the side bar and header when a page is printed.

As such, PDFs can be printed either through opening the print dialog and selecting "Save as PDF", or via traditional command-line conversion methods. For example, if your source content is Markdown, pandoc offers a method of converting from Markdown to PDF, including a Table of Contents:

```sh
pandoc --toc --latex-engine=xelatex source_file dest_file
```

## Tagged Documentation

The most straight-forward way to do this is through generating the documentation into different tagged folders into your source branch.

For example, after using `git tag` to select the desired release,

```sh
hugo --source=$SOURCE --destination=$DESTINATION
```

An example of this using a [gh-pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#enabling-github-pages-to-publish-your-site-from-master-or-gh-pages) branch can be found [here](https://github.com/CrunchyData/crunchy-containers/tree/gh-pages).
