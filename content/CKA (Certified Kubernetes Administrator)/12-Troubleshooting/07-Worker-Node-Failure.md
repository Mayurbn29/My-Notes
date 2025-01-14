---
date: 2024-04-05
last-modified: 2024-04-28
---
# Worker Node Failure

  - Take me to the [Lecture](https://kodekloud.com/topic/worker-node-failure/)

  - Lets check the status of the Nodes in the cluster, are they **`Ready`** or **`NotReady`**

    ```
    kubectl get nodes
    ```

  - If they are **`NotReady`** then check the **`LastHeartbeatTime`** of the node to find out the time when node might have crashed

    ```
    kubectl describe node worker-1
    ```

    ![wrk](wrk.PNG)


  - Check the possible **`CPU`** and **`MEMORY`**  using **`top`** and **`df -h`** 

 
    ![mem](mem.PNG)


  - Check the status and the logs of the **`kubelet`** for the possible issues.

    ```
    serivce kubelet status
    ```

    ```
    sudo journalctl -u kubelet
    ```
    ![kublet](kublet.PNG)
  
    
  - Check the **`kubelet`** Certificates, they are not expired, and in the right group and issued by the right CA.

    ```
    openssl x509 -in /var/lib/kubelet/worker-1.crt -text
    ```

    ![cert](cert.PNG)


