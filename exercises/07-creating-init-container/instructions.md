# Exercise 7

In this exercise, you will initialize a web application by standing up environment-specific configuration through an init container.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating an init container"](https://learning.oreilly.com/scenarios/4-1-ckad-multi-container/9781098104986/).

## Creating an Init Container

Kubernetes runs an init container before the main container. In this scenario, the init container retrieves configuration files from a remote location and makes it available to the application running in the main container. The configuration files are shared through a volume mounted by both containers. The running application consumes the configuration files and can render its values.

1. Create a new Pod in a YAML file named `business-app.yaml`. The Pod should define two containers, one init container and one main application container. Name the init container `configurer` and the main container `web`. The init container uses the image `busybox`, the main container uses the image `bmuschko/nodejs-read-config:1.0.0`. Expose the main container on port 8080.
See file
2. Edit the YAML file by adding a new volume of type `emptyDir` that is mounted at `/usr/shared/app` for both containers.
See file
3. Edit the YAML file by providing the command for the init container. The init container should run a `wget` command for downloading the file `https://raw.githubusercontent.com/bmuschko/ckad-crash-course/master/exercises/07-creating-init-container/app/config/config.json` into the directory `/usr/shared/app`.
See file. No need for shell, as these are not shell scripts?
4. Start the Pod and ensure that it is up and running.
Pod fails to initialise. Not sure what problem is. Old problems with multi-container pods?
Made some progress using a different command format - initContainer now works, but I'm not successfully downloading the files!
5. Run the command `curl localhost:8080` from the main application container. The response should render a database URL derived off the information in the configuration file.
6. (Optional) Discuss: How would you approach a debugging a failing command inside of the init container?