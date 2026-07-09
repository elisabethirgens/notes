---
layout: post
title: "Kustomize patching vs Helm templating"
date: 2026-07-08
---

…continuing from wrappig my head around [Kubernetes Objects]({{ '/2026/07/kubernetes-objects/' | url }}) and the different [types of objects]({{ '/2026/07/k8s-object-types/' | url }}), I&nbsp;can see my understanding of Kustomize and Helm starting to take form. Also how Argo CD fits into all of this. Progress!! 😤 A few days ago, my mental model was basically that the location for current YAML is a directory called `kustomize` and “the SRE team talks about something **migrating to Helm** something”.

Today I understand that Kustomize and Helm are two different approaches to writing Kubernetes Objects. Both create the same output; YAML that Kubernetes uses for configuration. The approach for authoring these YAML files are different. Let’s learn more about that difference:

## Kustomize

A configuration management tool for Kubernetes. Open source project, not part of Kubernetes core, but it is an official sub-project. It is described as “native for Kubernetes” and is built into `kubectl`. Every file is plain YAML that can be validated as YAML. Start with a base, this file needs to be a complete Kubernetes object, a runnable manifest. With Kustomize, different values for different environments are handled by overlay with patch files. The patches can be fragments of a Kubernetes Object, but I need to provide Kustomize with enough info to indentify the base to merge into.

<!-- prettier-ignore -->
```yaml
# k8s-objects/kustomize/base/cheesecake/deployment.yaml
apiVersion: apps/v1
kind: Deployment          # Required to be a valid Kubernetes Object
metadata:
  name: cheesecake        # Required to be a valid Kubernetes Object
spec:
  replicas: 1
```

<!-- prettier-ignore -->
```yaml
# k8s-objects/kustomize/prod/cheesecake/deployment-patch.yaml
apiVersion: apps/v1
kind: Deployment          # Required for Kustomize to know which base to patch
metadata:
  name: cheesecake        # Also for Kustomize to match against the correct base
spec:
  replicas: 5             # Moar pods in production, plz
```

In addition, we need a handful of `kustomization.yaml` files that point to the necessary resources and patches. These files are used by Kustomize for assembling the YAML. I can think of them as build-tool config, and should understand that these are never sent as Kubernetes Objects to the cluster.

```yaml
# k8s-objects/kustomize/base/cheesecake/kustomization.yaml
resources:
  - deployment.yaml
```

```yaml
# k8s-objects/kustomize/prod/cheesecake/kustomization.yaml
resources:
  - ../../base/cheesecake
patches:
  - path: deployment-patch.yaml
```

## Helm

Also a tool to manage configuration for Kubernetes and the one I am migrating to. Helm uses a different approach for creating the same output. I see that Helm is described as a package manager for Kubernetes. Not sure if this is important context for me working on migrating my applications. I suspect not, because “all the different ways to use Helm” is not my scope today. I want to follow the pattern set up by the SRE team and understand as much as possible about what I am doing. I need to write new YAML files. These will be different than the current Kustomize files and I need to know that Helm can provide Kubernetes with exactly the same manifests as before. The SRE team has set up Helm charts to be reused across applications, aswell as templates with placeholders. The template itself is not valid YAML, it needs values that I write in value files for my applications.

Another key difference, is that Helm charts are designed for reuse. The SRE team has created template files that can be used by many applications. A `default-cake` template that I can reuse for both `cheese-cake` and `chocolate-cake` on my team.

<!-- prettier-ignore -->
```yaml
# k8s-objects/helm/default-cake/Chart.yaml
apiVersion: v2
name: default-cake
version: 0.1.0                         # Version of this Helm Chart
```

<!-- prettier-ignore -->
```yaml
# k8s-objects/helm/default-cake/templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment                       # Template for a deployment object
metadata:
  name: default-cake
spec:
  replicas: {% raw %}{{ .Values.replicas }}{% endraw %}     # Placeholder looking for a value
```

Our organisation has chosen the approach where the values for Helm are now written in the application repo, not in the shared repo for Kubernetes Objects. So now all that 👆 gets abstracted away into shared charts and templates. Making the individual application values 👇 easier to discover and maintain by developers on the team who owns the app, in the application repo next to the source code.

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values.yaml

replicas: 1                            # Just the values, not a full object
```

<!-- prettier-ignore -->
```yaml
# cheesecake/helm/values-prod.yaml

replicas: 5                            # Different value for the template
```

Curious to see how it will be to work with values separated out into different repos. When I first heard about the intention, it made sense to me. Developers on teams who own the applications need to take responsibility for their application configuration. Seems great to manage the numer of replicas, CPU, memory, secrets and so on, closer to the source code.

## Difference wrapped up

Now that I understand way more about Kubernetes manifests, the benefit of using Helm is less clear to me. I’m sure there are plenty, I just don’t see them yet. Kustomize seems simpler in a way, more straight forward. But perhaps this is mainly because I now understand it better. 🙃

|           | Kustomize                                                | Helm                                                                             |
| :-------- | :------------------------------------------------------- | :------------------------------------------------------------------------------- |
| tooling   | built into `kubectl`                                     | separate binary for Helm CLI                                                     |
| reuse?    | not so much                                              | Helm charts are specifically designed for reuse across apps                      |
| base      | valid YAML that is runnable                              | template with placeholders for values                                            |
| env       | handled by overlay with patches                          | handled with value files to complete the template                                |
| logic     | nope                                                     | if / loops with Go template syntax                                               |
| discovery | explicit where `kustomization.yaml` points to every file | implicit for templates (auto discovery due to directory) and explicit for values |
