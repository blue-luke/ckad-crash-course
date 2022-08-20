# Exercise 6

In this exercise, you will create a ServiceAccount and assign it to a Pod.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating and assigning a ServiceAccount"](https://learning.oreilly.com/scenarios/3-7-ckad-security/9781098104962/).

## Using a ServiceAccount

1. Create a new service account named `backend-team`.
k create sa backend-team 
2. Print out the token for the service account in YAML format.
k get secret backend-team-token-dh7s7 -o yaml
3. Create a Pod named `backend` that uses the image `nginx` and the identity `backend-team` for running processes.
k run pod --image=nginx --serviceaccount=backend-team
--serviceaccount= is deprecated. Specify in yaml, or use --overrides='{ "spec": { "serviceAccountName": "backend-team" } }'
Accidentally called the service backed-team intially
4. Get a shell to the running container and print out the token of the service account.
ServiceAccount token is automounted /var/run/secrets/kubernetes.io/serviceaccount/token, had to look at docs to find this out, wasn't obvious 
Getting different tokens, not massively worried, synchronisation problem>
