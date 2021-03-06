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
git clone https://github.com/CrunchyData/crunchy-hugo-theme.git themes/crunchy-hugo-theme
```

### Option 2: Download

Download from https://github.com/CrunchyData/crunchy-hugo-theme and place the root folder in `themes`

### Option 3: git submodule

If you are working in a git project you can add the theme as a submodule:

```sh
git submodule add https://github.com/CrunchyData/crunchy-hugo-theme themes/crunchy-hugo-theme
```

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
ordersectionsby = "weight" # ordersectionsby = "title"
disableHomeIcon = false # default is false
disableSearch = false # default is false
disableNavChevron = false # set true to hide next/prev chevron, default is false
highlightClientSide = false # set true to use highlight.pack.js instead of the default hugo chroma highlighter
menushortcutsnewtab = false # set true to open shortcuts links to a new tab/window
enableGitInfo = true

[outputs]
home = [ "HTML", "RSS", "JSON"]

# Add additional URLs to the side nav here
# [[menu.shortcuts]]
# pre = "<h3>More</h3>"
# name = "<i class='fa fa-github'></i> <label>Github repo</label>"
# identifier = "ds"
# url = "https://github.com/CrunchyData/your-repo"
# weight = 10
#
# [[menu.shortcuts]]
# name = "<i class='fa fa-cloud-download'></i> <label>Download</label>"
# url = "https://github.com/CrunchyData/your-repo/releases/download/version/your-repo.2.6.tar.gz"
# weight = 11
```

#### Custom CSS

To add a custom CSS file to your project to override or add to the global styles, in your `/hugo/data/` directory, create a new configuration file 
named `css.toml`. The complete relative path name should resemble `/hugo/data/css.toml`.

Inside `css.toml`, a single line of code should be defined:

```sh
file = "main.css"
```

where `"main.css"` is the name of the custom CSS file. The theme will automatically look for this custom CSS file **only** in the `/hugo/static/css/` directory.

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

## Content Structure

Hugo has a few explicit requirements when it comes to content structure.

If you had a website structure similar to the following:

```sh
Home
About
- Meet the Team
Location
- Venue
- Hotel
Contact Us
```
Your Hugo content/ directory would need to resemble the following:

```sh
content/
-- about/
-------- meet-the-team.md
-------- _index.md
-- location/
-------- venue.md
-------- hotel.md
-------- _index.md
-- contact-us.md
-- _index.md
```

Static singular side pages can reside in the root of the content/ folder. This would include the contact-us.md file. Any website directories that will contain sub-pages must have their own designated folders with \_index.md files defined as the root of that subdirectory.

The \_index.md file itself at the root of /content is the homepage for the website; it must follow that naming convention for Hugo to recognize it.

It's possible to define characteristics for each of these pages, such as their weight (to define their order), their website titles, whether or not they should be displayed on the side navigation pane, and so on. This is done using [front matter](https://gohugo.io/content-management/front-matter/).

An example of this would be the following segment of front matter for `about/_index.md`:

```sh
title: 'About Us'
weight: 1
draft: false
```

That segment of code would do the following:
- set the website title to "About Us", as well as the name on the side navigation bar for the subdirectory
- list "About Us" as being the first element on the side navigation
- tells Hugo that the page is not a draft, and it can be published

If for some reason a specific page should be excluded from the side navigation, you can add the following to the parameters:

```sh
hidden: true
```

More information on related topics:
- [Directory Structure](https://gohugo.io/getting-started/directory-structure/)
- [Content Management](https://gohugo.io/content-management/)
- [Hugo's Directory Structure Explained](https://www.jakewiesler.com/blog/hugo-directory-structure/)

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

An example of this using a [gh-pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#enabling-github-pages-to-publish-your-site-from-master-or-gh-pages) branch can be found [here](https://github.com/CrunchyData/crunchy-containers/tree/gh-pages). More information on the publishing process can be found [here](https://gohugo.io/hosting-and-deployment/hosting-on-github/#deployment-of-project-pages-from-your-gh-pages-branch).

## Google Analytics

There is an option to add specific Google Analytics code snippets. This can be done by adding in a new file (automatically ignored by GitHub, as a security precaution) called `google-analytics.html` in the `/layouts/partials` directory. This will automatically be inserted immediately after the <head> tag through the `baseof.html` file in the `/layouts/_default` directory.
