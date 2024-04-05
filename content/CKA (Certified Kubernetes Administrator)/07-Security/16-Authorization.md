# Authorization
  - Take me to [Video Tutorial](https://kodekloud.com/topic/authorization/)
  
In this section, we will take a look at authorization in kubernetes

## Why do you need Authorization in your cluster?
- As an admin, you can do all operations
  ```
  $ kubectl get nodes
  $ kubectl get pods
  $ kubectl delete node worker-2
  ```
  
  ![at1](at1_CKA.PNG)
  
## Authorization Mechanisms
- There are different authorization mechanisms supported by kubernetes
  - Node Authorization
  - Attribute-based Authorization (ABAC)
  - Role-Based Authorization (RBAC)
  - Webhook
  
## Node Authorization

  ![node-auth](node-auth_CKA.png)
  
## ABAC

  ![abac](abac_CKA.PNG)
  
## RBAC

  ![rbac](rbac_CKA.PNG)

## Webhook
  
  ![webhook](webhook_CKA.PNG)
  
## Authorization Modes
- The mode options can be defined on the kube-apiserver

  ![mode](mode_CKA.PNG)
  
- When you specify multiple modes, it will authorize in the order in which it is specified

  ![mode1](mode1_CKA.PNG)
  
  
  #### K8s Reference Docs
  - https://kubernetes.io/docs/reference/access-authn-authz/authorization/
  
