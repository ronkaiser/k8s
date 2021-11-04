CHAPTER 2.6
Deployments


In this lesson, we will look at creating a Deployment. We will see how we can use Deployments to manage ReplicaSets. We will look at versioning our Deployments and how a Deployment will gracefully roll out those new versions.

deployexample.yaml:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment 
  labels: 
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx 
    spec: 
      containers:
      - name: nginx
        image: darealmc/nginx-k8s:v1
        ports:
        - containerPort: 80
```