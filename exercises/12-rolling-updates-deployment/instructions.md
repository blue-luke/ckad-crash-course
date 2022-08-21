# Exercise 12

In this exercise, you will create a Deployment with multiple replicas. After inspecting the Deployment, you will update its parameters. Furthermore, you will use the rollout history to roll back to a previous revision.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenarios ["Creating and Manually Scaling a Deployment"](https://learning.oreilly.com/scenarios/6-5-ckad-deployments/9781098105235/) and ["Rolling Out a New Revision for a Deployment"](https://learning.oreilly.com/scenarios/6-6-ckad-deployments/9781098105242/).

## Performing Rolling Updates for a Deployment

1. Create a Deployment named `deploy` with 3 replicas. The Pods should use the `nginx` image and the name `nginx`. The Deployment uses the label `tier=backend`. The Pods should use the label `app=v1`.
Deployment metadata as tier: backend
spec has matchLabels app: v1
template metadata has labels app: v1
2. List the Deployment and ensure that the correct number of replicas is running.
Fine
3. Update the image to `nginx:latest`.
k edit deploy deploy
(Can also update image imperatively, can't remember how) kubectl set image deployment/deploy nginx=nginx:latest
4. Verify that the change has been rolled out to all replicas.
Fine - k get pod X -o yaml to find image
5. Scale the Deployment to 5 replicas.
k scale deploy deploy --replicas=5
6. Have a look at the Deployment rollout history.
k rollout history deploy
Or, a specific version: kubectl rollout history deploy --revision=2
7. Revert the Deployment to revision 1.
k rollout undo deployment deploy 
Perhaps better to specific what you are reverting to: kubectl rollout undo deployment/deploy --to-revision=1
(I can carry out the above command many times. Not sure what it gets rolled back to the subsequent times)
8. Ensure that the Pods use the image `nginx`.
Pods use nginx. But there are still 5 of them. rollout undo doesn't undo scaling
9. (Optional) Discuss: Can you foresee potential issues with a rolling deployment? How do you configure a update process that first kills all existing containers with the current version before it starts containers with the new version?
- Additional load. Need to specifiy max available, max unavailable
- Have 2 versions of the app live at the same time. What if they're incompatible? Eg rely on different database schemas? So, the upgrades have to be backwards compatible
- Could set max unavailable as all - this would work but is clumsy. Use the recreate strategy. All existing Pods are killed before new ones are created when .spec.strategy.type==Recreate