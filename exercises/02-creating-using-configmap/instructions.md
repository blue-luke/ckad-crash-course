# Exercise 2

In this exercise, you will first create a ConfigMap from predefined values in a file. Later, you'll create a Pod, consume the ConfigMap as environment variables and print out its values from within the container.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a ConfigMap and consuming it as environment variables"](https://learning.oreilly.com/scenarios/3-3-ckad-configuration/9781098104917/).

## Configuring a Pod to Use a ConfigMap

1. Create a new file named `config.txt` with the following environment variables as key/value pairs on each line.

- `DB_URL` equates to `localhost:3306`
- `DB_USERNAME` equates to `postgres`

vi config.txt
DB_URL=localhost:3306

2. Create a new ConfigMap named `db-config` from that file.
k create configmap bd-config --from-file=./config.txt
3. Create a Pod named `backend` that uses the environment variables from the ConfigMap and runs the container with the image `nginx`.
(see pod file). Took some time to find out how to consume all key-value pairs from a cm as env variables
4. Shell into the Pod and print out the created environment variables. You should find `DB_URL` and `DB_USERNAME` with their appropriate values.
This is not working and I don't know where the problem is
Should have used --from-env-file
5. (Optional) Discuss: How would you approach hot reloading of values defined by a ConfigMap consumed by an application running in Pod?
Update cm file 
Kill pod and restart to pick up new config