---
date: 2024-04-05
last-modified: 2024-04-28
---
# Pods
  - Take me to [Video Tutorial](https://kodekloud.com/topic/pods-2/)
  
In this section, we will take a look at PODS.
- POD introduction
- How to deploy pod?

#### Kubernetes doesn't deploy containers directly on the worker node.

  ![pod](pod.PNG)
  
#### Here is a single node kubernetes cluster with single instance of your application running in a single docker container encapsulated in the pod.

![pod1](pod1.PNG)

#### Pod will have a one-to-one relationship with containers running your application.

  ![pod2](pod2.PNG)
  
## Multi-Container PODs
- A single pod can have multiple containers except for the fact that they are usually not multiple containers of the **`same kind`**.
  
  ![pod3](pod3.PNG)
  
## Docker Example (Docker Link)
  
  ![pod4](pod4.PNG)
  
## How to deploy pods?
Lets now take a look to create a nginx pod using **`kubectl`**.

- To deploy a docker container by creating a POD.
  ```
  $ kubectl run nginx --image nginx
  ```

- To get the list of pods
  ```
  $ kubectl get pods
  ```

 ![kubectl](kubectl.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/concepts/workloads/pods/pod/
- https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/
- https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/


