# HW4: Short Answers

Answer each question in 2-3 sentences.

## 1. Rolling-update safety
Why does the Deployment use `maxUnavailable: 0`, and what would change if it were `maxUnavailable: 1`?

`maxUnavailable: 0` keeps all three replicas available until a replacement pod is ready, so the rollout does not reduce the number of pods serving requests. With `maxUnavailable: 1`, Kubernetes could take one pod out of service before its replacement is ready, leaving two available for a while.

## 2. Health probes
Why do the liveness/readiness probes target `/health` instead of `/predict`?

`/health` lets Kubernetes check that the API is responding without running a prediction or relying on Redis. `/predict` does the actual scoring work, so a slow request or unavailable dependency could make a healthy pod look unhealthy if Kubernetes used it for a probe.

## 3. Autoscaling under load
Your HPA scales at 40% CPU up to 8 pods. If request volume doubled, what would you expect to happen? What happens once the HPA reaches its maximum?

If the extra requests push average CPU use above 40% of the pods’ CPU requests, the HPA will add pods, up to eight. Scaling takes time and depends on available metrics. Once it reaches eight, it cannot add more; if those pods cannot handle the traffic, CPU use may stay high and requests may take longer or fail.

## AI assistance disclosure
I used ChatGPT to help me understand the assignment rubric and Kubernetes settings, review the manifest changes, and draft these answers. I also used it to troubleshoot the deployment scripts and fix an image architecture incompatibility that prevented the app from starting in my local cluster. I checked the final work against the assignment and used the explanations to confirm my understanding.
