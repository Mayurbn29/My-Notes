# Static Pods 
  - Take me to [Video Tutorial](https://kodekloud.com/topic/static-pods/)
  
In this section, we will take a look at Static Pods

#### How do you provide a pod definition file to the kubelet without a kube-apiserver?
- You can configure the kubelet to read the pod definition files from a directory on the server designated to store information about pods.

## Configure Static Pod
- The designated directory can be any directory on the host and the location of that directory is passed in to the kubelet as an option while running the service.
  - The option is named as **`--pod-manifest-path`**.
  
  ![sp](sp_CKA.PNG)
  
## Another way to configure static pod 
- Instead of specifying the option directly in the **`kubelet.service`** file, you could provide a path to another config file using the config option, and define the directory path as staticPodPath in the file.

  ![sp1](sp1_CKA.PNG)

## View the static pods
- To view the static pods
  ```
  $ docker ps
  ```
  ![sp2](sp2_CKA.PNG)

#### The kubelet can create both kinds of pods - the static pods and the ones from the api server at the same time.

  ![sp3](sp3_CKA.PNG)

## Static Pods - Use Case

  ![sp4](sp4_CKA.PNG)
  
  ![sp5](sp5_CKA.PNG)
  
## Static Pods vs DaemonSets

   ![spvsds](spvsds_CKA.PNG)
  

#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/
