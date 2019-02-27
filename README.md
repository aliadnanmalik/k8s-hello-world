# Simple Flask Python HelloWorld Application

Simple Python app that listen to port 8080 and binds to 0.0.0.0 and answer "Hello World!" via HTTP

## First steps
Run the application locally:
```
virtualenv env
source env/bin/activate
pip3 install -r requirements.txt
python3 main.py
```

### Docker image build
Build it:
```
docker build . --tag python-hello-app
```

Run it:
```
docker run -d -p 0.0.0.0:8080:8080 python-hello-app
```

Use it:
```
curl localhost:8080
```


### DockerHub push image
Tag it:
```
docker tag python-hello-app:latest sinvalvm/python-hello-app
```

Push it:
```
docker push sinvalvm/python-hello-app
```

Pull it:

```
docker image pull sinvalvm/python-hello-app:<tag-name>
```

### Kubernetes
Deploy it:
```
kubectl apply -f k8s/kubernetes_deployment.yaml
kubectl apply -f k8s/kubernetes_service.yaml
```

Expose it:
```
kubectl expose deployment python-hello-app-deployment --type=LoadBalancer --port=8080
minikube service python-hello-app-deployment
```


```
Kubernetes exercise
1. Deploy a real application - OK
  1.1 Python/Go backend application - OK
    1.1.1 Publish it to DockerHub - OK
      $ docker tag python-hello-app:latest sinvalvm/python-hello-app
      $ docker push sinvalvm/python-hello-app
      $ docker image pull sinvalvm/python-hello-app
  1.2 Update Deployments for the backend - OK
    1.2.0 Update the version of the application - OK
    1.2.1 Increase number of replicas - OK
    1.2.2 Decrease number of replicas - OK
    1.2.3 Kill one of the pods and see how Kube take care of this scenario - OK
    1.2.4 Enter a container and sabotage the application - OK (could not kill the process PID 1)
    1.2.5 Enter a container and try to decay its performance - OK (used python $benchmark script and Rust Drill to load test it)
    1.2.6 Enter a container and mess with the OS (delete important files) - OK
    1.2.7 Enter a Pod and kill a healthy container - OK
    1.2.8 Enter a Pod and kill an unhealthy container - OK
    1.2.9 Update the version of the application but inserting a "bug" that make the app crash - OK (crashed without the healthcheck probe)
```
