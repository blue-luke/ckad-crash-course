# Exercise 5

In this exercise, you will create a ResourceQuota with specific CPU and memory limits for a new namespace. Pods created in the namespace will have to adhere to those limits.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a resource quota for a number of Secrets"](https://learning.oreilly.com/scenarios/3-6-ckad-security/9781098104955/).

## Defining a Pod’s Resource Requirements

Create a resource quota named `app` under the namespace `rq-demo` using the following YAML definition in the file `rq.yaml`.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: app
spec:
  hard:
    pods: "2"
    requests.cpu: "2"
    requests.memory: 500Mi
```

1. Create a new Pod that exceeds the limits of the resource quota requirements e.g. by defining 1Gi of memory but stays below the CPU e.g. 0.5. Write down the error message.
k create deployment dep --image=nginx --replicas=1 -n rq-demo
k set resources deployment/dep --requests=memory=1Gi,cpu=500m -n rq-demo
Not sure what error message they want
Could also specify requests in yaml and upload to an ns that already has the quota applied. That might produce the error message
2. Change the request limits to fulfill the requirements to ensure that the Pod could be created successfully. Write down the output of the command that renders the used amount of resources for the namespace.
k set resources deployment/dep --requests=memory=450Mi,cpu=500m -n rq-demo
k describe ns rq-demo
