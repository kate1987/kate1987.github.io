# Lightrun Documentation

## Introduction and Structure

This repo used the [mkdocs](https://github.com/mkdocs/mkdocs) static site generator with the [Material for MkDocs](https://github.com/squidfunk/mkdocs-material) theme, and specifically the [Insiders version](https://squidfunk.github.io/mkdocs-material/insiders/). It is published using [GitHub Pages](https://pages.github.com/) at https://docs.lightrun.com.

MkDocs is geared towards building *project documentation*. Documentation source files are written in a special flavor of Markdown, and configured with a single `mkdocs.yml` configuration file that holds the table of contents, and maps the main menu into the specific Markdown files - you can read more about how it all works [here](https://www.mkdocs.org/user-guide/writing-your-docs/#writing-your-docs).

This repository is currently maintained by [Quadri Sheriff](mailto:quadris@lightrun.com).

## Getting ready to work with the documentation repo

In order to work with the docs you'd need to have a local version of the repo and the `mkdocs` CLI installed.
The full steps for making a commit: 

1. Clone the repo - `git clone git@github.com:lightrun-platform/documentation.git`

1. Install `python3` - `sudo apt-get install python3` (or `brew install python@3.9`)

1. Make sure `pip` (`pip3`, to be exact) is installed  - `python3 -m pip --version` (note we're using the bundled version and not a standalone version - all modern Python distributions come with `pip` [installed by default](https://pip.pypa.io/en/stable/installing/)).

1. Use this repo's requirements file to install `mkdocs`, the `mkdocs-material` theme and all their neccessary dependencies - `python3 -m pip install -r requirements.txt`

If you have issues installing dependencies, you can try doing them one-by-one - refer to the extensions library documentation [here](https://facelessuser.github.io/pymdown-extensions/installation/)).

## Editing the documentation

Keep in mind that building the docs is a three part process (to be simplified using push-to-deploy in the future):

1. Write your documentation in Markdown (optionally adding new ones or re-arranging the structure of the docs using the `mkdocs.yml` file)
2. Build the repo (`mkdocs build`)
3. Publish the site (`mkdocs gh-deploy`)

The actual full list of steps, with a few more instructions:
1. Edit the relevant Markdown file under `/docs`. Note, that while the folder has a one-level hierarchy (i.e., all files are in the same folder without sub-folders), the _actual_ documentation site has a multi-level hierarchy (i.e., pages can be nested in other pages). The `mkdocs.yml` file contains this hierarchy - in order to understand where the Markdown file you're editing actually "sits" in practice, `grep` for it in `mkdocs.yml`. 
1. Note that MkDocs uses a somewhat unique flavor of Markdown - see guidelines [here](https://www.mkdocs.org/user-guide/writing-your-docs/#writing-with-markdown).
1. Once you've made your edits and you're satisfied with the location of the file in the hierarchy, you can validate how the page will look like in real life by running `python3 -m mkdocs serve`. This will build the docs site and serve a local version to `localhost:8000` - navigate to your page and verify you're happy with the outcome.  
1. Build the website (i.e. generate HTML & CSS from the Markdown) using `python3 -m mkdocs build`
1. Deploy to https://docs.lightrun.com using `python3 -m mkdocs gh-deploy` - this will trigger a GitHub pages deployment, which means a built version of the site will be pushed to the `gh-pages` branch and deployed.
1. If you haven't done so already, don't forget to commit your changes using `git add . && git commit -m"<YOUR-COMMIT-MESSAGE>" && git push`.

   A future version will have push to deploy instead of this cumbersome manual process.

### WARNINGS

MkDocs checks whether you have broken links and unused files when building the site.
This means that if you make a change (e.g., change a file name or add / edit a link) you might end up with a bunch of `WARNINGS` in your shell at build time.

**Please** make sure to remove all broken links and unused files before committing your PR to the repo - PRs that introduce new warnings will not be accepted.

#### A note about symlinking

If you symlink a file to re-use it (see [here](#re-using-entire-pages---symlinking-content)) and don't use the original file anywhere else, you'll get a warning. That's fine - please disregard it.
## Unused docs

A folder called `docs-unused`, in this repo, contains a bunch of older / irrelevant documentation.
It is intended for re-use once the documentation is properly updated - please ignore it for now, but don't delete it.

Hosting these files outside the main `docs` folder has the benefit of removing `WARN`s from the output of MkDocs as you build / serve your docs. If you'd like to use any of the docs in the `docs-unused` folder, remember to move them into the `docs` folder before adding their details to `mkdocs.yml`!

## Callouts

The Material theme for MkDocs employs the  term 'admonitions' for callouts. See the documentation for inserting admonitions [here](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#superfences).
## Re-using content

Sometimes you may wish to re-use a specific piece of content somewhere in the docs. For example, you want to use the same "Create an Account" page in Lightrun for Python and Lightrun for Node (since they both follow the same account registration process).  

To re-use _an entire page_, you can **symlink** content.  To re-use _parts of a page_ you can use **partials**.

### Re-using entire pages - Symlinking content

MkDocs, by default, treats each page as its own entity. That means, if you re-use a page in two different parts of the navigation structure, such as in the example above for the "Create an Account" page, you'll encounter a few problems: 

- When someone selects the "Create an Account" page inside Lightrun for Node, it will also auto-select the "Create an Account" page inside Lightrun for Python (and vice versa).
- If you duplicate the page across multiple categories, you'll have to edit all of them whenever you want to make a change. 

To solve this, we can create a single page under the root (`/docs`) directory and **symlink** to pages in other categories.

For example, for the "Create an Account" page, you'll notice there's a file called `create-account.md` in `/docs`. In addition, you'll note that in `mkdocs.yml` each runtime has its own "file":

```yaml
  - Lightrun for JVM :
    - Create an Account : 'jvm/create-account.md'
```

```yaml
  - Lightrun for Python :
    - Create an Account : 'python/create-account.md'
```

```yaml
  - Lightrun for Node.js :
    - Create an Account : 'node/create-account.md'
```

If you open the  `jvm/create-account.md`, `python/create-account.md`, and `node/create-account.md` files, you'll notice that each contains just the text ```../create-account.mda```, which is the symlink to the original `create-account.md`.  

When```create-account.md```in the root directory is updated,  the jvm, python, and node versions are updated too. 

When I want to add a reference to it in a new place, for example in Lightrun for Ruby, I can create a symlink, i.e.:

```shell
 ln -s create-account.md ruby/create-account.md
```

And then edit the `mkdocs.yml` appropriately:

```yaml
  - Lightrun for Ruby :
    - Create an Account : 'ruby/create-account.md'
```

### Embedding content - using snippets

There is a method to re-use portions of another file in your current file, using a Markdown extension called [Snippets](https://facelessuser.github.io/pymdown-extensions/extensions/snippets/).

All snippets are located in the `ux-reference` folder, which is _outside_ the main `docs` folder.

To add a snippet, insert at the required position in the text the following (after replacing the example file name): 

```
--8<-- "ux-reference/xxx-role-only.md"
```

A couple of notes:

1. There isn't a specific format for snippets - any valid markdown will do.
1. If you use a snippet inside a document and a link inside the snippet gets broken, you will get a WARNING when trying to build / serve the site. It **will not** be apparent that this link is from the snippet - so if you look for the link and can't find it in the doc, search inside the snippet.



## Documentation Style Guide

[Presentation link](https://docs.google.com/presentation/d/1dNkc9CrJb2S4lTsZpvASaeryUWWzXXA6xUWtc75J9vg/edit#slide=id.gbb87ee462b_1_0)

### Guideline 1 - Write docs, not wikis
<details>
  <summary>
    Expand!
  </summary>
<br/>

* The documentation website is, for all intents and purposes, marketing material
* The wiki is for internal consumption - it’s intended to share information between developers inside the company 
* The documentation is for external consumption - it’s intended to convince developers outside the company that Lightrun is a solid product that can solve their problems (and then simply be helpful once they’re convinced)  

#### 👍  Awesome!

> Lightrun supports Python V2.7 and Python V3.6-3.9.

#### 👎  Less awesome...

> The python agent supports Python2.7 and Python3 (Subversions 3.6,3.7,3.8,3.9 are explicitly supported, **newer versions will probably work as well, but haven't been tested**).
</details>

### Guideline 2 - Write like you don’t know the product
<details>
  <summary>
    Expand!
  </summary>
<br/>

* When writing, imagine you are reading docs from a product you do not know as intimately as you know Lightrun  

#### 👍 Awesome!

> Lightrun allows you to add snapshots - you can think of them as “non-breaking” breakpoints.

#### 👎 Less awesome...

> Lightrun allows you to add snapshots.
</details>

### Guideline 3 - Write step-by-step instructions, not scripts
<details>
  <summary>
    Expand!
  </summary>
<br/>

* When adding instructions, briefly explain the purpose or expected result of each step (e.g., command) in a procedure

#### 👍 Awesome!


> 1. Clone the agent’s repo:
> 
>     ```bash
>     git clone https://github.com/athena-io/athena.git .
>     ```
> 
> 2. Open the agent’s source code folder:
> 
>     ```bash
>     cd athena/agent_src
>     ```
> 
> 3. Build the agent using the build script:
> 
>     ```bash
>     bash build.sh
>     ```

#### 👎 Less awesome...

> Build agent:
> 
> ```bash
> git clone https://github.com/athena-io/athena.git . &&
> cd athena/agent_src &&
> bash build.sh
> ```
</details>

### Guideline 4 - Links, links, links
<details>
  <summary>
    Expand!
  </summary>
<br/>

* Keep in mind that the users reading the docs are not always fully aware of EVERYTHING in the docs site
* Lead the way, by inserting smartly-placed cross-references (links) in actionable instructions

#### 👍 Awesome!

> View the output and [exceptions](https://example.com/1) directly [from the IDE](https://example.com/2) - or [from our app in the browser](https://example.com/3).

#### 👎 Less awesome...

> View the output and exceptions directly from the IDE - or from our app in the browser.
</details>

### Guideline 5 - When to use images
<details>
  <summary>
    Expand!
  </summary>
<br/>

* Generally speaking, screenshots are appropriate when the interaction with the GUI is either:
  * Not intuitive
  * Requires use of something the user doesn’t already know, like our web console
* Refrain from adding screenshots where code snippets will do. Code we can copy and paste is always better than code in an image
* However, when (like in our onboarding flow) images are critical for understanding what to do, make sure to add them

#### 👍 Awesome!
```bash
java -jar lightrunc.jar list-agents
```

#### 👎 Less awesome...
![alt text](https://i.ibb.co/nCD5nK8/Docs-at-Lightrun-Google-Slides.png)
</details>

### Guideline 6 - How to insert images
<details>
  <summary>
    Expand!
  </summary>
<br/>

* MkDocs supports HTML attributes
* We use the <figure> attribute to add images
* To add an image:
  * Add it to the assets/images folder with a descriptive name - e.g., `assets/images/webstorm-ide-plugin.png`
  * Insert it in the appropriate place using a relative path - note that the path is from the location of the .md file, not the eventual HTML file
  * Use the (default) `width=600`
  * Add a relevant caption
  * Add an alt attribute to the image (it's OK if it's the same as the caption)

#### 👍 Awesome!
```html
<figure>
    <img src="../assets/images/webstorm-ide-plugin.png" width="600" alt="The Lightrun WebStorm IDE Plugin" />
    <figcaption>The Lightrun WebStorm IDE Plugin</figcaption>
</figure>
```
  </details>

## Important Links

[Official MkDocs Documentation](https://www.mkdocs.org/)

[Latest MkDocs Release Notes](https://www.mkdocs.org/about/release-notes/)

[MkDocs Material Theme](https://github.com/squidfunk/mkdocs-material)
