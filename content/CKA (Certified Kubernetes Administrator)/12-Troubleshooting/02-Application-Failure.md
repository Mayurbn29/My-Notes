---
date: 2024-04-05
last-modified: 2024-04-28
---
# Application Failure
  
  - Take me to [Lecture](https://kodekloud.com/topic/application-failure/)

  - In this lecture we will go step by step in troubleshooting Application failure.

  - To check the Application/Service status of the webserver

    ```
    curl http://web-service-ip:node-port
    ```

    ![app](app.PNG)

  - To check the endpoint of the service and compare it with the selectors

    ```
    kubectl describe service web-service
    ```   

    ![svc](svc.PNG)


  - To check the status and logs of the pod

    ```
    kubectl get pod
    ```

    ```
    kubectl describe pod web
    ```

    ```
    kubectl logs web
    ```

  - To check the logs of the previous pod

    ```
    kubectl logs web -f --previous
    ```
    
    ![db](db.PNG)


  #### Hands on Labs

  - Lets troubleshoot the [Application](https://kodekloud.com/topic/practice-test-application-failure/)