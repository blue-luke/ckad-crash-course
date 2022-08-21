# Exercise 13

In this exercise, you will create a CronJob and render its executions.

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda scenario ["Creating a CronJob"](https://learning.oreilly.com/scenarios/6-10-ckad-jobs/9781098105297/).

## Creating a Scheduled Container Operation

1. Create a CronJob named `current-date` that runs every minute and executes the shell command `echo "Current date: $(date)"`.
Copied a cronjob, edited it, see file. But, getting an error: got "map", expected "string"
I need to put the final command in quotes so that the brackets would be managed correctly
Still don't understand what I'm doing with commands and args though
2. Watch the jobs as they are being scheduled.
3. Identify one of the Pods that ran the CronJob and render the logs.
k logs current-date-27684896-5tn42
Current date: Sun Aug 21 14:56:01 UTC 2022
4. Determine the number of successful executions the CronJob will keep in its history.
k get cronjob current-date -o yaml
successfulJobsHistoryLimit: 3
Also monitored which pods were live
5. Delete the Job.