# Exercise 1

In this exercise, you will practice the creation of a new Pod in a namespace. Once created, you will inspect it, shell into it and run some operations inside of the container.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating and interacting with a Pod"](https://learning.oreilly.com/scenarios/2-1-ckad-pods/9781098104818/).

## Creating a Pod and Inspecting it

1. Create the namespace `ckad-prep`.
k create namespace ckad-prep
2. In the namespace `ckad-prep`, create a new Pod named `mypod` with the image `nginx:2.3.5`. Expose the port 80.
k run mypod -n ckad-prep --image=nginx:2.3.5 --port=80
3. Identify the issue with creating the container. Write down the root cause of issue in a file named `pod-error.txt`.
echo Failed to pull image "nginx:2.3.5": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/nginx:2.3.5": failed to resolve reference "docker.io/library/nginx:2.3.5": docker.io/library/nginx:2.3.5: not found >> pod-error.txt
4. Change the image of the Pod to `nginx:1.15.12`.
k edit pod mypod -n ckad-prep
5. List the Pod and ensure that the container is running.
k get pod -n ckad-prep
6. Log into the container and run the `ls` command. Write down the output. Log out of the container.
k -n ckad-prep exec -it mypod -- /bin/sh
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
7. Retrieve the IP address of the Pod `mypod`.
k get pod -n ckad-prep -o wide
10.4.1.96
8. Run a temporary Pod in the namespace `ckad-prep` using the image `busybox`, shell into it and run a `wget` command against the `nginx` Pod using port 80.
(used nginx and curl instead)
9. Render the logs of Pod `mypod`.
k logs mypod -n ckad-prep
10. Delete the Pod and the namespace.
k delete namespace ckad-prep
k delete pod mypod -n ckad-prep
etc