# Managing Application Logs
  - Take me to [Video Tutorial](https://kodekloud.com/topic/managing-application-logs/)

In this section, we will take a look at managing application logs

#### Let us start with logging in docker

![ld](ld_CKA.PNG)
 
![ld1](ld1_CKA.PNG)
 
#### Logs - Kubernetes
```
apiVersion: v1
kind: Pod
metadata:
  name: event-simulator-pod
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
```
 ![logs-k8s](logs-k8s_CKA.png)
 
- To view the logs
  ```
  $ kubectl logs -f event-simulator-pod
  ```
- If there are multiple containers in a pod then you must specify the name of the container explicitly in the command.
  ```
  $ kubectl logs -f <pod-name> <container-name>
  $ kubectl logs -f even-simulator-pod event-simulator
  ```

  ![logs1](logs1_CKA.PNG)
  
#### K8s Reference Docs
- https://kubernetes.io/blog/2015/06/cluster-level-logging-with-kubernetes/
 
