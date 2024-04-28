---
date: 2024-04-05
last-modified: 2024-04-28
---
# Network Policies
  - Take me to [Video Tutorials](https://kodekloud.com/topic/network-policies-3/)
  
#### Trafic flowing through a webserver serving frontend to users an app server serving backend API and a database server

  ![traffic](traffic.PNG)
  
- There are two types of traffic
  - Ingress
  - Egress
  
   ![ing1](ing1.PNG)
  
   ![ing2](ing2.PNG)
  
## Network Security

  ![nsec](nsec.PNG)
  
## Network Policy

  ![npol](npol.PNG)
  
  ![npol1](npol1.PNG)
  
## Network Policy Selectors
  
  ![npolsec](npolsec.PNG)
  
## Network Policy Rules

  ![npol2](npol2.PNG)
  
## Create network policy
 
- To create a network policy
  ```
  apiVersion: networking.k8s.io/v1
  kind: NetworkPolicy
  metadata:
   name: db-policy
  spec:
    podSelector:
      matchLabels:
        role: db
    policyTypes:
    - Ingress
    ingress:
    - from:
      - podSelector:
          matchLabels:
            role: api-pod
      ports:
      - protocol: TCP
        port: 3306
  ```
  
  ```
  $ kubectl create -f policy-definition.yaml
  ```
  
 ![npol3](npol3.PNG)
 
 ![npol4](npol4.PNG)
  
## Note
 
 ![note1](note1.PNG)
 
#### Additional lecture on [Developing Networking Policies](https://kodekloud.com/topic/developing-network-policies/)

#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/services-networking/network-policies/
- https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/
 
  
  
  
  
