---
layout: post
title: "Deployment and other K8s Object Types"
date: 2026-07-07
---

…continuing from understanding the basics of [Kubernetes Objects]({{ '/2026/07/kubernetes-objects/' | url }}) yesterday, today I’m diving into the different object types for Kubernetes. Okay, so I get now that objects in the repo name `k8s-objects` is not only plural because we have many hundreds of apps, there are different types of objects. Specified in the `kind` field right at the top of the files. Two important object types are deployment and service.

## Deployment for creating pods

This is the object type that contain most of the fields I have typically worked with over the years.

<!-- prettier-ignore -->
```yaml
apiVersion: apps/v1
kind: Deployment           # Object type for creating pods
metadata:
  name: tivoli             # A name to identify the object in this YAML
spec:                      # Spec describes desired my state
  replicas: 3              # Create 3 pods and keep them running
```

## Service for networking

These files mention the name of my app multiple times, which has been a source of confusion before. Writing up this example now, helped me understand the difference between the fields.

<!-- prettier-ignore -->
```yaml
apiVersion: v1
kind: Service              # Object type for networking
metadata:
  name: tivoli             # A name to identify the object in this YAML
  namespace: tivoli        # The partition in the cluster where this object lives
spec:                      # Spec describes desired my state
  selector:
    app: tivoli            # Find these pods and send traffic to them
  ports:
    - protocol: TCP        # Default (not required unless other protocol than TCP)
      name: http           # Name optional / cosmetic if only one port
      port: 1234           # The service listens to this port
```

## Core built-in Kubernetes objects

This is not the comprehensive list, these are the types relevant for me to understand right now, because of how the applications I am migrating from Kustomize to Helm are currently set up.

| kind                  | apiVersion | description                                                                                                              |
| :-------------------- | :--------- | :----------------------------------------------------------------------------------------------------------------------- |
| Pod                   | v1         | The smallest deployable unit in Kubernetes. Not one I create directly, but an object I manage with a Deployment          |
| Deployment            | apps/v1    | Create and manage a set of pods, keep them running. Fields like replicas, CPU and memory, loads of environment variables |
| Service               | v1         | Provide stable internal address and load balance traffic, even as pods come and go. Ports go here.                       |
| ConfigMap             | v1         | Store non-sensitive configuration data, like env vars and config files that get injected into pods                       |
| Namespace             | v1         | Define a logical boundary to group and separate objects. Not an object I create in Git, but a value I use a lot          |
| PersistentVolume      | v1         | Represent storage in the cluster                                                                                         |
| PersistentVolumeClaim | v1         | Request storage, pods reference the PVC not the PV                                                                       |

## Custom Resources (CRDs)

And these are also relevant for me. These are not build-in to Kubernetes, they are added by tools. But they do create real objects that are submitted to the cluster.

| kind        | apiVersion                | description                                                                                       |
| :---------- | :------------------------ | :------------------------------------------------------------------------------------------------ |
| Application | argoproj.io/v1alpha1      | Tell ArgoCD which Git repo to watch and where to deploy. This object defines our GitOps pipeline  |
| Mapping     | getambassador.io/v3alpha1 | Tell the gateway which requests to catch and which Service to send them to                        |
| PodMonitor  | monitoring.coreos.com/v1  | Tell Prometheus which pods to scrape for metrics. For&nbsp;observability, not for running the app |

## Build-tool config

| kind          | apiVersion                      | description                                                        |
| :------------ | :------------------------------ | :----------------------------------------------------------------- |
| Kustomization | kustomize.config.k8s.io/v1beta1 | Config to describe how to assemble YAML, never sent to the cluster |

This last one is relevant for understanding more about the difference between Kustomize and Helm, which sounds like a great topic for tomorrow.
