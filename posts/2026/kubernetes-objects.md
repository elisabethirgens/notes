---
layout: post
title: "Kubernetes Objects"
date: 2026-07-06
---

I’m working on migrating a handful of applications from using Kustomize to Helm. Because the SRE team has requested teams to migrate their apps. This is part a larger effort to standardize how we configure, deploy and run our apps across the company. They have also written scripts to help teams migrate, but I’d like to _not_ throw stuff on the wall and cross my fingers while I see what sticks.

I want to understand what I am doing, and I suspect a good place to start, is by getting a better grasp of some Kubernetes fundamentals.

## K8s

Obligatory link to my description of [Numeronyms and Numerical Contractions]({{ '/2026/07/numeronyms/' | url }})

## Making changes to k8s-objects

We have a shared repo `k8s-objects` where I have opened and merged 84 PRs. Let’s see what type of changes I have been doing in there. The very first PR, was adding myself as a deployer 4½ years ago. Changing log levels on a couple of apps. A handful of PRs cleaning up leftover configuration for apps in test environments where an app wasn’t actually running.

Oh hey, I can see the PR which back in the day got me to set up the GitHub CLI. The `k8s-objects` README.md described that for changes to test environments, I could open PRs that are automatically approved and merged. _Shut up and take my money!_ Luckily, I didn’t understand at the time what triggered that behaviour in this repo, that I could have set the required label by clicking a button on the PR in the GUI. I just read the approach as running an incantation `gh pr create --label automerge` and so this was how I got around to setting up the GitHub CLI and start using that. Never looked back though, now I very much appreciate opening my PRs from the command line.

Another PR I remember, where I was increasing CPU and memory limits. In the PR description, I posted the meme photo of golden retriever in a tie who has no idea what he’s doing. We were just back at the office after covid and this PR description led to a friendly plattform developer dropping by my desk to say hi and have a chat about CPU and memory limits.

I’ve been doing a whole bunch of changes to ensure that memory requests are equal to memory limits. This has been based on a policy warning from Kyverno. Then there are the PRs that consist of “adding this thing” because someone has described the app needs this thing now. Also enabling OpenTelemetry tracing, this was an environment variable to set in application kustomize yaml.

Recently, I have been decommissioning a handful of applications. Working on that means I now know the recommended approach is to first delete the file(s) that configures the app in ArgoCD. Wait til after ArgoCD has synced, then open a separate PR to delete the app’s files in the kustomize directory.

## A Kubernetes object is a persistent record

An LLM described it to me like this:

> A Kubernetes object is a record you create describing something you want to exist or happen in your cluster. You write it down as YAML, and Kubernetes' job is to make reality match what you wrote. Think of it like filling out a form: "I want this to exist, with these properties." Kubernetes reads the form and does whatever it takes to make it true — and keeps checking forever that it stays true. Every object generally has the same skeleton:

<!-- prettier-ignore -->
```yaml
apiVersion: apps/v1
kind: Deployment           # What TYPE of object this is
metadata:
  name: cheesecake         # A name to identify it
spec:                      # What I want, my desired state
  replicas: 3              # I'd like 3 pods, plz
```

## spec vs status

> Kubernetes also tracks a `status` field (added automatically, not written by you) — that's the actual state. Kubernetes' entire job is constantly comparing `spec` (desired) vs `status` (actual) and reconciling the difference. This loop is the heart of how Kubernetes works.

I think all this means that I do know quite a bit about what Kubernetes objects actually are. It’s not some mysterious concept beyond my understanding. It was helpful to both read up a bit and revisit the changes I’ve been making in the `k8s-objects` repo over the past 4 years. Working on this migration means I want to understand more than I have before, but this adventure is off to a good start.
