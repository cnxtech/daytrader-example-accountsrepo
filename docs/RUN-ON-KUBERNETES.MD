
## Run on Kubernetes

### Build the Accounts

1.  `$ cd daytrader-accountsapp`

2.  `$ mvn -Pcd clean install`

    This command builds the Docker Image and pushes it to the DockerHub registry

### Start the Accounts

1.  `$ kubectl apply -f daytrader-accounts/env/external/k8s/deployment.yaml`

    This command pulls the image from DockerHub and deploys it to the Kubernetes Cluster
    
2.  `$ kubectl get pods --watch`
    
    NAME | READY | STATUS | RESTARTS | AGE
    ---- | ----- | ------ | -------- | ---
    daytrader-accounts-xxxxxxxxx-xxxxx | 1/1 | Running | 0 | 6m
    
    Watch until you see READY `1/1` and STATUS `Running` then Ctrl-c to stop watching
    
3.  `$ kubectl apply -f daytrader-accounts/env/external/k8s/service.yaml`

**TODO** Add a `deploy_server` shell script to run these commands. (See Run on Spring Boot)

### Test the Accounts
                                   
1.  `$ cd daytrader-accounts`

2.  `$ mvn -Pci-k8s clean install`

    This command starts the application, runs the integration tests, and stops the application

**TODO** Add a `ci-k8s` Maven profile to run the integration tests. (See Run on Spring Boot)
    
### Stop the Accounts

1.  `$ kubectl delete deployments daytrader-accounts`

2.  `$ kubectl delete services daytrader-accounts`

**TODO** Add an `undeploy_server` shell script to run these commands. (See Run on Spring Boot)

### Review the Swagger Documentation

1.  Start the Accounts

2.  `kubectl port-forward daytrader-accounts-xxxxxxxxx-xxxxx` 1888:1443

    You should see `Forwarding from 127.0.0.1:1888 -> 1443`
    
    This command forwards local port 1888 to port 1443 of your Pod

3.  Point you browser to `https://localhost:1888/swagger-ui.html`

4.  Stop the Accounts after reviewing the APIs


