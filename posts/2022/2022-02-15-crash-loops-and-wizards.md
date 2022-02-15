---
layout: post
title: "Crash Loops and Wizard Programmers"
date: 2022-02-15
---

[Julia Evans](https://twitter.com/b0rk/) has a zine called [So you want to be a wizard](https://wizardzines.com/zines/wizard/) about how she “approaches learning hard things and getting better at programming”. She has useful tips on debugging, reading unfamiliar code, building expertise, asking awesome questions. A helpful point she makes, that has stuck with me over the years, is **how your questions get less ignorant FAST**.

I had exactly this experience recently. My deploy caused a crash loop — and the question I asked that afternoon is quite different from questions I could ask now — only few workdays later.

I‘m currently 3 months into a new job, and this means all my experience from previous code bases and developer environments and systems are blending into the current state of the world around me, creating a mashup in my brain ranging from tranquil familiarity to weird misapprehensions.

Friday: I deploy an application. Next, a Kubernetes pod reports a `CrashLoopBackOff`. What ever that is. But they usually sport a much better sounding status of `Running`. I assume it may also be stuck in this state, because of the noise it’s generating on Slack. And with the added bonus of this being Friday afternoon, it doesn’t feel like the time to start poking around to pick up pieces of knowledge or experiment with what to do. It is the time for a question like:

👩🏻‍💻 “Halp. I have a CrashLoopBackOff. What do I do about that?”<br>
🧙🏻‍♂️ “A rollback would be nice! And here is how to check the logs from that pod.”

First thing for me to understand, was that yes, this was caused by my code change. That wasn't initially clear to me. Why not? I worked many years in the UI layer of Java apps, where any regressions I created would be visual — minor or quite spectacular — but there was little I worked on that created other types of errors. If the tests passed and I could build the app locally, anything that might go wrong after my deploy would be “something else” and not directly due to my change. These earlier years of working in systems where _my_ change to markup or styles are not the cause of a faulty deploy, has left some residue in my brain I need to get rid of. (Later I had a stint in a project working with OpenShift, where I learnt a boatload about pods and containers! With environment and tooling being early days, I vaguely recall that pods could get stuck without the reason being my code change also here.)

- **My previous misapprehension** — crash loop means something went haywire with my deploy, but the cause must be somewhere in the pipeline, outside the repo itself
- **Updated understanding** — thanks to helpful co-workers who explained that, yes, a crash loop can have many different causes, anything from code errors (like now!) to failing health checks

---

## CrashLoopBackOff

> CrashLoopBackOff is a status message that indicates one of your pods is in a constant state of flux—one or more containers are failing and restarting repeatedly.

> While it’s technically an error status, it’s more of an opportunity to investigate why containers in a pod are failing to attain the Running state.

This was a great read! [Understanding Kubernetes CrashLoopBackoff Events](https://www.containiq.com/post/kubernetes-crashloopbackoff)

## kubectl commands

```
# List pods in namespace cheesecake
kubectl get pods -n cheesecake

# Describe a specific pod with verbose output
kubectl describe pods <pod_name>

# Show logs from a specific running pod
kubectl logs -n cheesecake cheesecake-98765-abc
```

I see plenty more I will play around with, now that I know to look for commands on<br> [kubernetes.io/docs/reference/kubectl/cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

And if I break something I can’t fix, my questions will be substantially different from last Friday.
