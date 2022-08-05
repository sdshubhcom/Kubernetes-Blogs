# What is Pod and Why Kuberenetes use Pods?

Pod is a running process in cluster. It contains one or more container such as docker container. In pod containers are managed as single entity and share the resources. You can have different types of containers in a single pod whether it is related to application or database.

![image](https://user-images.githubusercontent.com/69069614/182211103-440cabac-ebbd-4feb-80d2-36a485d16525.png)

Kuberetes does not run contaiers directly intsead it run the pod and groups the containers and ensures that each of them use same resources and network.
The main purpose of using pods is **Replication.** When containers are grouped together into pod then with replication kubernetes can horizontally scale application as needed. In other words if a single pod is workload increases Kuberentes will make the replicas of it and will deploy to the cluster. This ensures that during heavy workload cluster will perfom effeciently and also by making replicas it provides failure resistence to the cluster.

**Pods in a Kubernetes cluster are used in two main ways :**

**1. Single container Pod**

Single container pod refers to the pod which contains only one container. you can deploy such pod by writing a yaml file. And running the kubectl command

```
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  namespace: websrvr
  labels:
    app: nginx
    tier: front
    version: v1
    env: production
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

Once the yaml file is created save the file let's give name **nginx.yaml** and run the create command to run the file.

```
kubectl create –f nginx.yml
```
It will create a pod with the name of nginx. We can use the describe command along with kubectl to describe the pod.

**Multi container Pod**

