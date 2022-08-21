# Exercise 14

In this exercise, you will create a Deployment and expose a container port for its Pods. You will demonstrate the differences between the service types ClusterIP and NodePort.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenarios ["Creating a Service of type ClusterIP"](https://learning.oreilly.com/scenarios/7-1-ckad-services/9781098105310/) and ["Creating a Service of type NodePort"](https://learning.oreilly.com/scenarios/7-2-ckad-services/9781098105327/).

## Routing Traffic to Pods from Inside and Outside of a Cluster

1. Create a Service named `myapp` of type `ClusterIP` that exposes port 80 and maps to the target port 80.
k create service clusterip myapp --tcp=80:80   
What does the tcp bit mean? I'm suprised to see tcp there

2. Create a Deployment named `myapp` that creates 1 replica running the image `nginx`. Expose the container port 80.
k create deployment myapp --image=nginx --replicas=80 --port=80 
I created 80 pods, not 2!

3. Scale the Deployment to 2 replicas.
 k scale deployment myapp --replicas=2

4. Create a temporary Pod using the image `busybox` and run a `wget` command against the IP of the service.
kubectl run pod --image=busybox --rm -it --restart=Never -- /bin/sh 
Review the above command. It creates a pod and execs into it immediately 
wget 10.8.12.46:80
Produces:
saving to 'index.html'
index.html           100% |**********************************************************************|   615  0:00:00 ETA
'index.html' saved
One can also execute the pod command from ones own terminal: kubectl run tmp --image=busybox --restart=Never -it --rm -- wget -O- 10.109.232.76:80

5. Change the service type so that the Pods can be reached from outside of the cluster.
Add an ingress to the service? Ingress is already true though. And there is no external ip atm
Apparently, turn it into a nodeport. Not sure how this means it can be accessed outside the cluster

Solution says ping the node and port. How do I know what node the nodeport service is on? Perhaps the service is on the same node as the deployments it servces? So, do k get pod -o wid, showing node of pods

6. Run a `wget` command against the service from outside of the cluster.
Can't do this, return to?

7. (Optional) Discuss: Can you expose the Pods as a service without a deployment?
Yes, label the pods and use that label in the service match selector

8. (Optional) Discuss: Under what condition would you use the service type `LoadBalancer`?
In the cloud
