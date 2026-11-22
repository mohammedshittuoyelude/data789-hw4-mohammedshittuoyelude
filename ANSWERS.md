# HW4 — Short Answers

Answer each question in 2–3 sentences.

## 1. Rolling-update safety
Why does the Deployment use `maxUnavailable: 0`, and what would change if it were `maxUnavailable: 1`?

With `maxUnavailable: 0`, Kubernetes keeps all three existing replicas available until a replacement pod is ready, which preserves serving capacity during the rollout. If it were `1`, Kubernetes could take one pod out of service before its replacement is ready, temporarily reducing capacity to two replicas.

## 2. Health probes
Why do the liveness/readiness probes target `/health` instead of `/predict`?

The `/health` endpoint gives Kubernetes a lightweight check that the API process is responding without running a fraud prediction or depending on Redis. The `/predict` endpoint does real scoring work, so using it as a probe could make a healthy pod look unhealthy when scoring is slow or a dependency is unavailable.

## 3. Autoscaling under load
Your HPA scales at 40% CPU up to 8 pods. If request volume doubled, what would you expect to happen — and what happens once it reaches the maximum?

If the higher request volume pushes average CPU utilization above 40% of the pods’ CPU requests, the HPA will add replicas, up to eight; scaling takes time and depends on reported metrics. At eight replicas, it cannot add more, so if that capacity is insufficient, CPU can remain above target and response times or errors may increase.

## AI assistance disclosure
I used ChatGPT to interpret the assignment rubric, explain Kubernetes resource limits, probes, autoscaling, and update strategies, and help draft and review the manifest changes and written explanations. I reviewed the changes and will verify that I can explain each part before submitting.
