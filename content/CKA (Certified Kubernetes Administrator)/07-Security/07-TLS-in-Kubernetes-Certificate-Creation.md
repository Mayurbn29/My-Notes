---
created: 2024-04-05
modified: 2024-04-05
---
# TLS in kubernetes - Certificate Creation
  - Take me to [Video Tutorial](https://kodekloud.com/topic/tls-in-kubernetes-certificate-creation/)
  
In this section, we will take a look at TLS certificate creation in kubernetes

## Generate Certificates
- There are different tools available such as easyrsa, openssl or cfssl etc. or many others for generating certificates.

## Certificate Authority (CA)

- Generate Keys
  ```
  $ openssl genrsa -out ca.key 2048
  ```
- Generate CSR
  ```
  $ openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
  ```
- Sign certificates
  ```
  $ openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
  ```
 
 ![ca1](ca1.PNG)
 
## Generating Client Certificates

#### Admin User Certificates

- Generate Keys
  ```
  $ openssl genrsa -out admin.key 2048
  ```
- Generate CSR
  ```
  $ openssl req -new -key admin.key -subj "/CN=kube-admin" -out admin.csr
  ```
- Sign certificates
  ```
  $ openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt
  ```
  
  ![ca2](ca2.PNG)
  
- Certificate with admin privilages
  ```
  $ openssl req -new -key admin.key -subj "/CN=kube-admin/O=system:masters" -out admin.csr
  ```
  
#### We follow the same procedure to generate client certificate for all other components that access the kube-apiserver.

  ![crt1](crt1.PNG)
  
  ![crt2](crt2.PNG)
  
  ![crt3](crt3.PNG)
   
  ![crt4](crt4.PNG)
  
## Generating Server Certificates

## ETCD Server certificate

  ![etc1](etc1.PNG)
  
  ![etc2](etc2.PNG)
  
## Kube-apiserver certificate

  ![api1](api1.PNG)
  
  ![api2](api2.PNG)
  
## Kubectl Nodes (Server Cert)

   ![kctl1](kctl1.PNG)
   
## Kubectl Nodes (Client Cert)

   ![kctl2](kctl2.PNG)
   
   
   
  
  

  

  


  
  
  
  
 
