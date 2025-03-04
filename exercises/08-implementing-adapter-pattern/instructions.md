# Exercise 8

In this exercise, you will implement the adapter pattern for a multi-container Pod.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a sidecar container"](https://learning.oreilly.com/scenarios/4-2-ckad-multi-container/9781098104993/).

## Implementing the Adapter Pattern

The adapter pattern helps with providing a simplified, homogenized view of an application running within a container. For example, we could stand up another container that unifies the log output of the application container. As a result, other monitoring tools can rely on a standardized view of the log output without having to transform it into an expected format.

1. Create a new Pod in a YAML file named `adapter.yaml`. The Pod declares two containers. The container `app` uses the image `busybox` and runs the command `while true; do echo "$(date) | $(du -sh ~)" >> /var/logs/diskspace.txt; sleep 5; done;`. The adapter container `transformer` uses the image `busybox` and runs the command `sleep 20; while true; do while read LINE; do echo "$LINE" | cut -f2 -d"|" >> $(date +%Y-%m-%d-%H-%M-%S)-transformed.txt; done < /var/logs/diskspace.txt; sleep 20; done;` to strip the log output off the date for later consumption by a monitoring tool. Be aware that the logic does not handle corner cases (e.g. automatically deleting old entries) and would look different in production systems.
See file
Major blocker in creating the pods. Error solved by changing use of command to args, and using the format in the file. This could have been what blocked all other attempts at multi-container pods
2. Before creating the Pod, define an `emptyDir` volume. Mount the volume in both containers with the path `/var/logs`.
See file
3. Create the Pod, log into the container `transformer`. The current directory should continuously write a new file every 20 seconds.
Not quite - the code wrote the time and date to the same file every 5 seconds