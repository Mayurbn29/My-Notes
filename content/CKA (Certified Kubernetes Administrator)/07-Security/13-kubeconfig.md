---
date: 2024-04-05
last-modified: 2024-04-28
---
# KubeConfig 
  - Take me to [Video Tutorial](https://kodekloud.com/topic/kubeconfig/)

In this section, we will take a look at kubeconfig in kubernetes


#### Client uses the certificate file and key to query the kubernetes Rest API for a list of pods using curl.
- You can specify the same using kubectl

  ![kc1](kc1.PNG)
  
- We can move these information to a configuration file called kubeconfig. And the specify this file as the kubeconfig option in the command.
  ```
  $ kubectl get pods --kubeconfig config
  ```
  
## Kubeconfig File
- The kubeconfig file has 3 sections
  - Clusters
  - Contexts
  - USers
  
  ![kc4](kc4.PNG)
  
  ![kc5](kc5.PNG)
  
- To view the current file being used
  ```
  $ kubectl config view
  ```
- You can specify the kubeconfig file with kubectl config view with "--kubeconfig" flag
  ```
  $ kubectl config veiw --kubeconfig=my-custom-config
  ```
  
  ![kc6](kc6.PNG)
  
- How do you update your current context? Or change the current context
  ```
  $ kubectl config use-context <context-name>
  ex: 
  $ kubectl config use-context prod-user@production
  ```
  
  ![kc7](kc7.PNG)
  
- kubectl config help
  ```
  $ kubectl config -h
  ```
  
  ![kc8](kc8.PNG)
  
## What about namespaces?

  ![kc9](kc9.PNG)
 
## Certificates in kubeconfig

  ![kc10](kc10.PNG)
 
  ![kc12](kc12.PNG)
  
  ![kc11](kc11.PNG)
 
#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config
