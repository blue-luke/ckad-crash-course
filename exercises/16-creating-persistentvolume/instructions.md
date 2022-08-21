# Exercise 16

In this exercise, you will create a PersistentVolume, connect it to a PersistentVolumeClaim and mount the claim to a specific path of a Pod.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a Pod with Volume of type PersistentVolume with static binding"](https://learning.oreilly.com/scenarios/8-2-ckad-volumes/9781098105365/).

## Defining and Mounting a PersistentVolume

1. Create a Persistent Volume named `pv`, access mode `ReadWriteMany`, storage class name `shared`, 512Mi of storage capacity and the host path `/data/config`.
(Host path won't work in multi-node clusters. But I don't think I could do this exercise anyway. I don't know how to enter the host path, not found in documents)
2. Create a Persistent Volume Claim named `pvc` that requests the Persistent Volume in step 1. The claim should request 256Mi. Ensure that the Persistent Volume Claim is properly bound after its creation.
3. Mount the Persistent Volume Claim from a new Pod named `app` with the path `/var/app/config`. The Pod uses the image `nginx`.
All created
4. Check the events of the Pod after starting it to ensure that the Persistent Volume was mounted properly.
failed to generate spec: failed to mkdir "/data/config": mkdir /data: read-only file system
This is probably the error above, ie no host paths on multinode clusters
Possible also GKE not letting you write to the control plane node file system
