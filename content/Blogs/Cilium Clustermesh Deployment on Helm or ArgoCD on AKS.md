##### This guide describes the setup for configuring Cilium Cluster Mesh between 2 AKS clusters running with Cilium CNI.


Cilium Version: v1.15.4

This is discussed in much more detail in these GitHub issues:  
[https://github.com/cilium/cilium/issues/19057](https://github.com/cilium/cilium/issues/19057)   
[https://github.com/cilium/cilium/issues/32076](https://github.com/cilium/cilium/issues/32076)

Reference: https://docs.kubermatic.com/kubermatic/v2.25/tutorials-howtos/networking/cilium-cluster-mesh/ (This is an older version of cilium and some values are irrelevant.)


##### <u>Pre-Requisites</u>:

 - 2 Clusters deployed on AKS

 - The AKS cluster must be created with `--network-plugin none`. See the [Bring your own CNI](https://docs.microsoft.com/en-us/azure/aks/use-byo-cni?tabs=azure-cli) documentation for more details about BYOCNI prerequisites / implications.
 
 - PodCIDR ranges in all clusters and all nodes must be non-conflicting and unique IP addresses.
    
- Nodes in all clusters must have IP connectivity between each other using the configured InternalIP for each node. This requirement is typically met by establishing peering or VPN tunnels between the networks of the nodes of each cluster.
    
- The network between clusters must allow the inter-cluster communication. The exact ports are documented in the [Firewall Rules](https://docs.cilium.io/en/stable/operations/system_requirements/#firewall-requirements) section.
##### <u>Steps to create clustermesh on Helm or ArgoCD</u>:    

1. <u>Deploy Cilium and Clustermesh on the First Cluster using these values</u>:

   ```yaml	
    aksbyocni:
	  enabled: true
	nodeinit:
	  enabled: true
	cluster:
	  name: primary-aks-cluster
	  id: 1
	ipam:
	  operator:
	    clusterPoolIPv4PodCIDRList: ["10.10.0.0/16"]
	clustermesh:
	  useAPIServer: true
	  apiserver:
	    service:
	      type: LoadBalancer
	      annotations:
	        service.beta.kubernetes.io/azure-load-balancer-internal: "true"
	    tls:
	      auto:
	        enabled: true
	        method: cronJob
	        schedule: 0 0 1 */4 *
    ```

<br>

2. <u>Retrieve Cluster Mesh data from Cluster 1</u>:      
    **In Cluster 1**, retrieve the information necessary for the next steps:


    - Retrieve CA cert & key:

      ```
      kubectl get secret cilium-ca -n kube-system -o yaml
		```
	

    - Retrieve clustermesh-apiserver external IP:

	    ```
      kubectl get secret cilium-ca -n kube-system -o yaml
        ```
<br>

3. <u>Get the base64 encoded CA cert and key and the clustermesh-apiserver ip address from the first cluster and add it to the helm values in the second cluster</u>:

   ```yaml
	aksbyocni:
	  enabled: true
	nodeinit:
	  enabled: true
	cluster:
	  name: secondary-aks-cluster
	  id: 2
	ipam:
	  operator:
	    clusterPoolIPv4PodCIDRList: ["10.20.0.0/16"]
	tls:
	  ca:
	    cert: "<cert>"
	    key: "<key>"
    clustermesh:
	  config:
	    enabled: true
	    clusters:
	    - name: primary-aks-cluster
	      port: 2379
	      ips:
	      - 192.168.10.5
	  useAPIServer: true
	  apiserver:
	    service:
	      type: LoadBalancer
	      annotations:
	        service.beta.kubernetes.io/azure-load-balancer-internal: "true"	
	    tls:
	      auto:
	        enabled: true
	        method: cronJob
	        schedule: 0 0 1 */4 *
	operator:
	  replicas: 1
    ```

<br>

4. <u>Repeat Step 2 for Cluster 2, Retrieve Cluster Mesh data from Cluster 2</u>:    

    **In Cluster 2**, retrieve the information necessary for the next steps:

    - Retrieve CA cert & key:

      ```
      kubectl get secret cilium-ca -n kube-system -o yaml
		```
	

    - Retrieve clustermesh-apiserver external IP:

	    ```
      kubectl get secret cilium-ca -n kube-system -o yaml
        ```
<br>

5. <u>Get the Service IP Address from the second cluster and add it under the config section in the helm values for the first cluster:</u>


   ```yaml
	aksbyocni:
	  enabled: true
	nodeinit:
	  enabled: true
	cluster:
	  name: primary-aks-cluster
	  id: 1
	ipam:
	  operator:
	    clusterPoolIPv4PodCIDRList: ["10.10.0.0/16"]
	clustermesh:
	  config:
	    enabled: true
	    clusters:
	    - name: secondary-cluster
	      port: 2379
	      ips:
	      - 192.168.20.5
	  useAPIServer: true
	  apiserver:
	    service:
	      type: LoadBalancer
	      annotations:
	        service.beta.kubernetes.io/azure-load-balancer-internal: "true"
	    tls:
	      auto:
	        enabled: true
	        method: cronJob
	        schedule: 0 0 1 */4 *
	```
	
<br>


6. <u>Check Cluster Mesh status:</u>    

   At this point, check Cilium health status in each cluster with:
	  ```
	  kubectl exec -it cilium-<pod-id> -n kube-system -- cilium-health status
   ```
   
   It should show all local and remote cluster’s nodes and not show any errors. It may take a few minutes until things settle down since the last configuration.


> [!note] Note: 
> It may also help to manually restart:
> - first `clustermesh-apiserver` pods in each cluster,
> - then `cilium` agent pods in each cluster.