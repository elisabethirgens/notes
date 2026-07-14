---
layout: post
title: "Supply Values When Installing A Helm Chart"
date: 2026-07-13
---

……continuing from learning more about [Kubernetes Objects]({{ '/2026/07/kubernetes-objects/' | url }}), the different [types of objects]({{ '/2026/07/k8s-object-types/' | url }}) and how [Kustomize vs Helm]({{ '/2026/07/kustomize-and-helm/' }}) handles environments. Loads of things are starting to make sense.

And yet a couple of pieces of this puzzle have been incredibly confusing. Sometimes it is the “this is supposed to be straight forward” stuff that is the most confusing, when they just fail to be straight forward in my head. I could have just made it work and moved on with my life, but I stubbornly insist on understanding. I think I can now explain to myself what my confusion was about. Let’s give it a go:

## What was clear 👌

The SRE team in my org has created a Helm chart with templates for a `default-cake` application. My&nbsp;job is make sure my applications fill in their values when installing that chart. The steps for migrating from Kustomize to Helm, is to supply my app `cheesecake` with something like:

- `cheesecake/helm/shared.yaml`
- `cheesecake/helm/values-prod.yaml`
- `cheesecake/helm/values-test.yaml`

Note: these file names are made up by me, the actual files need to use different names that correspond with names defined in a specific template. I am doing this on purpose for the sake of these notes, because it is helpful for me to properly understand what is arbitrary and what is semantic.

## What I’ve been confused about

There was documentation and plenty examples in other applications for me to look at. That can sometimes cause as much confusion as clarity. They can be written by someone who understands what is what just fine and might not need to think too much about naming. They might know that “it doesn’t really matter” and that turns into someone else’s confusion. That for example `default` is an arbitrary name. Or no, wait! In my context it is semantic. 😅 It was arbitrary for the author of the Helm chart, but not for me, I have a dependency to the chart templates, so I need to know that `default` is a convention in my ecosystem and now semantic.

```yaml
environmentDefinitions:
  literal:
    config: {}

deployment:
  useEnvironment:
    literal:
      config: ""
```

What is exactly is `config`? 🤔 Okay, this is a field that I can and should name in my application. For example `cheesecake`. Or `cheesecake-env` that I see some apps use. Right, not too hard to figure out that I can call it whatever I want. And that it doesn’t matter much what name I pick.

What is the difference between these two `config` fields? Why is one empty like this `config: {}` and the other like so `config: ""` ? I found examples that differentiated between `cheesecake` for shared values and `cheesecake-vary` for values that vary between environments, which seemed like a good idea, but also… I’d be looking at three different files for values, with a handful of different keys defined, and now we haven’t even mentioned secrets. Which values override where between different files?!?

Getting clear on all this eluded me for a while. And I can see now that it _really_ tripped me up a year ago. Another source of confusion, is when examples from other apps can be authored by someone who copy-pasted something they kinda misunderstood, but hey — it works fine and so inconsistency is planted and left to confuse others later. I am responsible for some of those, I’ve been looking at edits I made a year ago to a couple of Helm-files, and choices I made then are super weird. Which is why it is motivating to see that I can read these files with way better comprehension today.

## What I understand better now

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

environmentDefinitions:
  literal:
    cheesecake:           # Map the following values to a key using this name
      CAKE_ENABLED: true
      ASSET_URL: https://cdn.cakefactory.com

deployment:
  useEnvironment:
    literal:
      cheesecake: ""      # Wire in any values from the key with this name
```

- `environmentDefinitions.literal` is where the key is named and defined, and it is also where I list the actual environment variables relevant to write in this file
- `deployment.useEnvironment.literal` is where the key is used, and where the values are wired in to the Kubernetes object that is Deployment

This is an abstraction that intends on making it easier for developers on application teams to write their value files. The way I think about it now, is that in a stripped down example, the abstraction becomes an extra loop to wrap my head about. But I suspect this set up does some useful wiring behind the scenes, and that this becomes especially helpful when it comes to secrets.

### Empty examples

I started by looking at the most basic applications. That didn’t quite help me. Because I got a bit hung up on trying to decide an approach for naming these keys and grouping the variables. The basic apps didn’t need to define additional variables, so I made it more difficult for myself by wanting to document empty examples in the files. The idea being that I could pick a pattern and apply the same approach to all 10 apps. Now I know that this would do the trick to define a mapping key even though it is currently empty.

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

environmentDefinitions:
  literal:
    cheesecake: {}        # Define a mapping key, currently explicitly empty

deployment:
  useEnvironment:
    literal:
      cheesecake: ""      # Empty string for no prefix added to variable names
```

I also understand now that the empty string is a completely different kind of empty. This is an option in our set up where it is possible to add a prefix to the variable names. That prefix would follow the naming all the way into the cluster. Good to know if I later come across any usecase for a prefix.

### The order doesn’t matter

I could tell by looking at examples in other team’s apps that the order can be whatever.

That doesn’t stop me from wanting to form an opinion and being consistent. It seems like many prefer to list `deployment` first, then any other fields, and lastly the `environmentDefinitions` at the bottom. Perhaps because the migration script creates that order? The documentation writes it the other way around. Which is the order that makes sense to me now that I understand which field defines the key, and where it is wired in. Data first, then activation. Anyway. I will stop overthinking now and follow the order created by the migration script. That will probably become the order expected by most.

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

deployment:
  useEnvironment:
    literal:
      cheesecake: "" # This key will wire in values from environmentDefinitions

environmentDefinitions:
  literal:
    cheesecake: {}   # Define a mapping key for useEnvironment.literal
      # Add environment variables below and pssst remove the {} above ;-)
      # CAKE_ENABLED: true
      # ASSET_URL: https://cdn.cakefactory.com

```

### Overrides

All right. With this understanding in place, and this written up so I can check my own notes later, I&nbsp;am ready to figure out how I should use the different value files, how to group the variables and name the keys. Try not to overthink, but just think about it a tiny bit more. Enough to make a deliberate choice.
