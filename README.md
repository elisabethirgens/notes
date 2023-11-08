# My notes

Eleventy and GitHub Pages to write notes

## Deploy

- https://github.com/peaceiris/actions-gh-pages

### Configure a publishing source

Under Settings for GitHub Pages, use the `publish_branch` named in `.github/workflows/build.yml` as the publishing source.

### Link to a previous post

```
[link text]({{ '/2020/09/to-all-jobs-i-had-before/' | url }})
```
