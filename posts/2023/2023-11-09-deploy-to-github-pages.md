---
layout: post
title: "Deploy Eleventy to GitHub Pages"
date: 2023-11-09
---

I’m taking my [minimalist Eleventy project starter]({{ '/2023/11/minimalist-eleventy/' | url }}) and putting the example site on the air! GitHub Pages is a free hosting service with many limitations, and perfectly fine for an Eleventy project that already lives in a GitHub repository. Let’s publish my `tiny11ty` demo site with these 4 steps:

## Step 1: add a workflow

- Create a `.github/workflows/build-and-deploy.yml` (example in [this commit](https://github.com/elisabethirgens/tiny11ty/commit/06168c69eeb16d480a81d59d3f7521ccb3bbe234))
- Find the Actions tab: [github.com/elisabethirgens/tiny11ty/actions](https://github.com/elisabethirgens/tiny11ty/actions/)

This will now run a job to build ✅ while the job to deploy will fail ❌

## Step 2: change repo setting

- Go to the repo’s Settings > Pages > Build and deployment
- and select **Source: GitHub Actions**

This will make absolutely nothing happen quite yet. Why? Because the workflow describes that the action is triggered on push to the main branch. Or that it can be run manually.

```
on:
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
```

## Step 3: make action run again

- Push a new change to the main branch
- (or run workflow manually with **Re-run jobs** at the upper right of the Actions tab)

This will now build and deploy and I can see my page.

- The repo at [github.com/elisabethirgens/tiny11ty](https://github.com/elisabethirgens/tiny11ty) becomes…
- A page published to: [elisabethirgens.github.io/tiny11ty](https://elisabethirgens.github.io/tiny11ty/)

But after step 3 something is looking very wrong 😱 There is no CSS and the link to the example post is broken, sending me to a 404 page. Why?&nbsp;Because we need to handle this Eleventy gotcha:

## Step 4: path prefix with subdirectory

- Edit the `eleventy.config.js` to return a `pathPrefix`
- Add `pathPrefix` to the build script in `package.json`

Find code examples in [this commit](https://github.com/elisabethirgens/tiny11ty/commit/69ec97a9d87e572aa6f3eb933c3f969625e137dd), or dive into in the full explanation at [11ty.dev/docs/config](https://www.11ty.dev/docs/config/#deploy-to-a-subdirectory-with-a-path-prefix)

And with that, the build and deploy should be a wrap 💝

---

### GitHub Pages before and now

It can be confusing to find examples and references that show how this worked before. At the time of writing, the other option in the repo settings for source is “deploy from branch” which is described as ‘the classic experience’. This would
be with using an external plugin, and then to deploy from a publishing source that was typically a special `gh-pages` branch.

### Beta?

I am curious why the approach I’m using is still in beta when it is now 470 days since [Custom GitHub Actions Workflows](https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/) was released.

### Disable the Jekyll build?

Another GitHub Pages quirk with the ‘classic experience’ option with a `gh-pages` branch, was that Jekyll was assumed. So if using something other than Jekyll, it was necessary to disable the Jekyll build by adding an empty file `.nojekyll` to the root of the pages repo. Aw, [Jekyll](https://jekyllrb.com/)… I kinda miss Jekyll, but I don’t miss having to maintain installations of Ruby solely for the purpose of working with a static site generator. This is where [Eleventy](https://www.11ty.dev/docs/get-started/) is my jam 🎈
