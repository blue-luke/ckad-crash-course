# Exercise 11

In this exercise, you will exercise the use of labels and annotations for a set of Pods.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenarios ["Assigning labels to Pods imperatively"](https://learning.oreilly.com/scenarios/6-1-ckad-labels/9781098105181/) and ["Assigning annotations to Pods imperatively"](https://learning.oreilly.com/scenarios/6-3-ckad-annotations/9781098105204/).

## Defining and Querying Labels and Annotations

1. Create three different Pods with the names `frontend`, `backend` and `database` that use the image `nginx`.
k run frontend --image=nginx
etc

2. Declare labels for those Pods as follows:

- `frontend`: `env=prod`, `team=shiny`
- `backend`: `env=prod`, `team=legacy`, `app=v1.2.4`
- `database`: `env=prod`, `team=storage`

k label pod frontend env=prod team=shiny
etc

Could also do:
kubectl run frontend --image=nginx --restart=Never --labels=env=prod,team=shiny

3. Declare annotations for those Pods as follows:

- `frontend`: `contact=John Doe`, `commit=2d3mg3`
- `backend`: `contact=Mary Harris`

k annotate pod frontend contact="John Doe" commit=2d3mg3
etc

4. Render the list of all Pods and their labels.
k get pods --show-labels
5. Use label selectors on the command line to query for all production Pods that belong to the teams `shiny` and `legacy`.
k get pods -l team=shiny && k get pods -l team=legacy
Presume he means 'shiny or legacy'
I neglected to also restrict it to prod pods. Better:
kubectl get pods -l 'team in (shiny, legacy)',env=prod --show-labels
6. Remove the label `env` from the `backend` Pod and rerun the selection.
k label pod backend env-
7. Render the surrounding 3 lines of YAML of all Pods that have annotations.
Not sure