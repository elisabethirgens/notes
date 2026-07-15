---
layout: post
title: "The Cake Is A Lie and Other Overrides"
date: 2026-07-14
---

…continuing from understanding how to [Supply Values When Installing A Helm Chart]({{ '/2026/07/helm-charts/' | url }}). The next step is getting clear on how to group the variables and name the keys. Note to self: don’t overthink this, but think about it just enough to form an opinion and make a deliberate choice. I want to be consistent across all the apps I will be migrating from Kustomize to Helm.

For the sake of these notes, I can consider these three files in my app `cheesecake`

- `cheesecake/helm/shared.yaml` for shared default values that apply to all environments
- `cheesecake/helm/values-prod.yaml` for overrides to a production environment
- `cheesecake/helm/values-test.yaml` for overrides to a test environment

Remember that the actual file names I need to use are different from this example, the names are defined in a template that my apps will be using. The important part is that Helm has a mechanism for merging. Sounds like it works basically like the cascade in CSS, just without any concept of specificity. A later value will override an earlier value.

## Potential override problems

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/shared.yaml

environmentDefinitions:
  literal:
    cheesecake:
      CAKE_ENABLED: true
      ASSET_URL: https://cdn.cakefactory.com
```

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

environmentDefinitions:
  literal:
    cheesecake:
      CAKE_ENABLED: false
      ASSET_URL: https://cdn.cakefactory.com
```

Disabling cake is definitely a mistake. In a long file, this override can be difficult to spot. Humans reading the first file will think cake is enabled when that would be a lie. What happens when the CDN changes? A&nbsp;developer might edit the value in `shared.yaml` and then get tripped up by why that didn’t work. Kubernetes doesn’t care and neither of these are the end of the world. But is it possible to avoid?

## A possible improvement

The pattern I’ve seen used in some apps, is to separate the variables into groups. For example, one group named `cheesecake` for what is shared across environments, and another group `cheesecake-vary` intended for everything that will vary per environment.

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/shared.yaml

environmentDefinitions:
  literal:
    cheesecake:                  # collection shared across environments
      CAKE_ENABLED: true         # enable cake for all environments 
```

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

environmentDefinitions:
  literal:
    cheesecake-vary:             # vary collection for prod
      ASSET_URL: https://cdn.cakefactory.com
```

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-test.yaml

environmentDefinitions:
  literal:
    cheesecake-vary:             # vary collection for test
      ASSET_URL: https://cdn-test.cakefactory.com
```

I like this. It is an attempt at naming the collection with more intent. And yet… there is nothing to enforce it, or to ensure that future-me (or others) understand what current-me meant by the `-vary` suffix.

## Nope, lets rely on the file structure

Looking at this again now, after understanding a whole lot more about how to [Supply Values When Installing A Helm Chart]({{ '/2026/07/helm-charts/' | url }}), I think the different files already do the job. Yes, it’s very possible to make a confusing mess with misunderstandings and duplicates, but that can happen just as much with this attempt at naming a group with `-vary`.

My first meeting with Helm value files, I got really tripped up by finding overrides with the same values and overrides with different values that were not intentional and also duplicates that were a mistake. So it was alluring to come across a possible improvement. Now that I understand the override mechanism better, I will stick with embracing the structure in the files themselves — and use a single key named `cheesecake`. Perhaps I will come across other use cases later that change my mind, but for now I like the idea of just letting the different files guide which environment variables belong where, and stick with one name for this key. Now it feels like I definitely did overthink this, but I found comments I wrote on PRs a year ago, that remind me about how confused I was. It feels good to now understand that confusion, and also have resolved it properly.

Ready for the next step… 🥁 secrets form the secret manager and mounting configuration files.
