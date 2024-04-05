# API Groups
  - Take me to [Video Tutorial](https://kodekloud.com/topic/api-groups/)
  
In this section, we will take a look at API Groups in kubernetes

## To return version and list pods via API's 

 ![api3](api3_CKA.PNG)
 
- The kubernetes API is grouped into multiple such groups based on their purpose. Such as one for **`APIs`**, one for **`healthz`**, **`metrics`** and **`logs`** etc.

  ![api4](api4_CKA.PNG)
 
## API and APIs
- These APIs are catagorized into two.
  - The core group - Where all the functionality exists
    
    ![api5](api5_CKA.PNG)
 
  - The Named group - More organized and going forward all the newer features are going to be made available to these named groups.
  
    ![api6](api6_CKA.PNG)
    
- To list all the api groups

  ![api7](api7_CKA.PNG)
  
## Note on accessing the kube-apiserver
- You have to authenticate by passing the certificate files.

  ![api8](api8_CKA.PNG)
  
- An alternate is to start a **`kubeproxy`** client
  
  ![api9](api9_CKA.PNG)
  
## kube proxy vs kubectl proxy
 
  ![kp](kp_CKA.PNG)
  
## Key Takeaways

  ![api10](api10_CKA.PNG)

#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/
- https://kubernetes.io/docs/reference/using-api/api-concepts/
- https://kubernetes.io/docs/tasks/extend-kubernetes/http-proxy-access-api/
