---
date: 2024-04-05
last-modified: 2024-04-28
---
# Static Pods 
  - Take me to [Video Tutorial](https://kodekloud.com/topic/static-pods/)
  
In this section, we will take a look at Static Pods

#### How do you provide a pod definition file to the kubelet without a kube-apiserver?
- You can configure the kubelet to read the pod definition files from a directory on the server designated to store information about pods.

## Configure Static Pod
- The designated directory can be any directory on the host and the location of that directory is passed in to the kubelet as an option while running the service.
  - The option is named as **`--pod-manifest-path`**.
  
  ![sp](sp.PNG)
  
## Another way to configure static pod 
- Instead of specifying the option directly in the **`kubelet.service`** file, you could provide a path to another config file using the config option, and define the directory path as staticPodPath in the file.

  ![sp1](sp1.PNG)

## View the static pods
- To view the static pods
  ```
  $ docker ps
  ```
  ![sp2](sp2.PNG)

#### The kubelet can create both kinds of pods - the static pods and the ones from the api server at the same time.

  ![sp3](sp3.PNG)

## Static Pods - Use Case

  ![sp4](sp4.PNG)
  
  ![sp5](sp5.PNG)
  
## Static Pods vs DaemonSets

   ![spvsds](spvsds.PNG)
  

#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/
