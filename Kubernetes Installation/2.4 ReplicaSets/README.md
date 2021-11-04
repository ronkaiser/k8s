CHAPTER 2.4
ReplicaSets

In this lesson, we will take a look at ReplicaSets. We will look at the file structure of the YAML file that is used to create the ReplicaSet, as well as how to scale and delete ReplicaSets.

Contents of replicas-example.yaml:
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: nginx
    tier: frontend
spec:
  replicas: 2
  selector:
    matchLabels: 
      tier: frontend
    matchExpressions:
      - {key: tier, operator: In, values: [frontend]}
  template:
    metadata:
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: darealmc/nginx-k8s:v1
        ports:
        - containerPort: 80
```