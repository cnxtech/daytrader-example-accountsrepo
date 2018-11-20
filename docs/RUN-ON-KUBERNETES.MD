
## Run on Kubernetes

### Build the Accounts

1.  `$ cd daytrader-accountsapp`

2.  `$ mvn -Pcd clean install`

    This command builds the Docker Image and pushes it to the DockerHub registry

### Start the Accounts

1.  `$ cd daytrader-accounts/env/external/k8s`

2.  `$ kubectl apply -f deployment.yaml`

    This command pulls the image from DockerHub and deploys it to the Kubernetes Cluster
    
3.  `$ kubectl get pods --watch`
    
    NAME | READY | STATUS | RESTARTS | AGE
    ---- | ----- | ------ | -------- | ---
    daytrader-accounts-xxxxxxxxx-xxxxx | 1/1 | Running | 0 | 6m
    
    Watch until you see READY `1/1` and STATUS `Running` then Ctrl-c to stop watching
    
3.  `$ kubectl apply -f service.yaml`

Currently, these commands are run manually, but they can easily be added to Maven

### Test the Accounts
                                   
1. Access the Swagger UI for testing the APIs
    
### Stop the Accounts

1.  `$ cd daytrader-web\env\external\k8s`

2.  `$ kubectl delete deployments daytrader-accounts`

3.  `$ kubectl delete services daytrader-accounts`

Currently, these commands are run manually, but they can easily be added to Maven

### Access the Swagger UI

1.  Start the Accounts

2.  `kubectl port-forward daytrader-accounts-xxxxxxxxx-xxxxx`

    You should see `Forwarding from 127.0.0.1:8888 -> 1443`
    
    This command forwards local port 8888 to port 1443 of your Pod

3.  Point you browser to `https://localhost:1443/swagger-ui.html`

4.  Stop the Accounts after reviewing (or testing) the APIs


