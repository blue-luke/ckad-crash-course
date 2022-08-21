# Exercise 9

In this exercise, you will create a Pod running a NodeJS application. The Pod will define readiness and liveness probes with different parameters.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a Pod with a readiness Probe of type HTTP GET request"](https://learning.oreilly.com/scenarios/5-1-ckad-probing/9781098105105/).

## Defining a Pod’s Readiness and Liveness Probe

1. Create a new Pod named `hello` with the image `bmuschko/nodejs-hello-world:1.0.0` that exposes the port 3000. Provide the name `nodejs-port` for the container port.
See file
2. Add a Readiness Probe that checks the URL path / on the port referenced with the name `nodejs-port` after a 2 seconds delay. You do not have to define the period interval.
See file
3. Add a Liveness Probe that verifies that the app is up and running every 8 seconds by checking the URL path / on the port referenced with the name `nodejs-port`. The probe should start with a 5 seconds delay.
See file. I created each section in steps, running $ k apply -f FILE --dry-run=client after each, to check yaml and make it easier to find bugs
4. Shell into container and curl `localhost:3000`. Write down the output. Exit the container.
Output = Hello World
5. Retrieve the logs from the container. Write down the output.
Magic happens on port 3000

Overlooked the 8 second period on the liveness probe!
Note - I'm not clear on how the pod can ping itself on localhost:3000. Clarify understanding. Is localhost just a way of accessing a server locally?
