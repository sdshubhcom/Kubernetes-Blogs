# What is ReplicaSet ?

ReplicaSet object is used to maintain a stable set of replicated pods running within a cluster at any given time. Its purpose is to maintain the specified number of pods and prevent the user from loosing the control of the application in case of any pod failure or inaccessible. Whenever any pod gets failed replicaset immediately launches another pod and replacing it with failed pod.

![rs6](https://user-images.githubusercontent.com/69069614/197348646-c191b79d-9e02-43c8-beab-4b33b6b8566e.png)

**Replicaset has following features:**
- A pod template is used to create a new pod whenever an existing pod fails and also replica count is also maintained by defining the desired number of replicas that a controller needs to be running.
- A replica set also ensures that additional pod needs to be created or deleted whenever instance with same label is created.
- Replcaset allows to have multiple replicas of pod which means that the traffic is sent to different instances which prevents single instance from being overloaded.
- Replcaset ensures it has multiple replicas of application so that it won't fail because of one pod fails.

## Replicaset Configuration

**Below is the yaml file which will create multi replicas of pod.**

```
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replica
  namespace: facebook
spec:
  replicas: 4
  minReadySeconds: 10
  selector:
    matchLabels:
      role: web
    matchExpressions:
      - {key: version, operator: In, values: [v1, v2, v3]}
  template:
    metadata:
      name: web
      labels:
        role: web
        version: v1
        tier: frond
    spec:
      containers:
      - name: web
        image: httpd
        ports:
        - containerPort: 80
          protocol: TCP
```

**Fields that are use to define replicaset are as follows:**

- **Selector:** It is used to identify for which pod the replicaset is responsible for.
- **Replicas:** It specifies the number of pods which replicaset has to maintain.
- **Template:** It defines the pod template that replicaset will use in order to create new pods.
- **ApiVersion:** It defines kubernetes API that supports ReplicaSet.

# What is Deployment ?
Deployment is use to maintain the versions of your application running in the pod. It helps to efficiently scale the number of replica pods and enable the rollout and rollback to an earlier deployment version. Deployments runs on multiple replicas of the pod and automatically replaces a pod in case of any failure or unresponsive. In this way Deployments helps to ensure that one or more instances of your application are available to serve user requests. 

Deployments use a Pod template, which contains a specification for its Pods. The Pod specification determines how each Pod should look like: what applications should run inside its containers, which volumes the Pods should mount, its labels, and more. When a Deployment's Pod template is changed, new Pods are automatically created one at a time.

![image](https://user-images.githubusercontent.com/69069614/197216181-fb953a23-60f9-4131-8392-2c7818fb6134.png)

## What are Rolling Update and Rollback in Deployment ?

Basically, Rolling update provides the orderly migration from one version to a newer version. Rolling update is used in such situation when a new version of application came and you have to switch to a newer version. In the rolling update all the running pod will be replaced with the newer version of application by systematically terminating the older version of application pods.

Rollback on the other hand is used to roll back to older version of your application. Suppose you have a new bug in the application that needs to be solved in that case you might need to go to the older version of the application with rollback you can achieve that. With rollback all the replicas of the pod which are running on the new version of the application will be rollback again to previous version.

# Deployment with Replicaset

Deploymens are generelly used with replicaset as they are used to manage replicsets. With the help of deployment You can simply roll back to a previous Deployment revision. When you are managing ReplicaSet using Deployment You can also use a Deployment to create a new revision of a ReplicaSet and then migrate existing pods from an older revision into the new revision. After that, the Deployment can take care of cleaning up old, unused ReplicaSets.

So, Replicaset ensure replicas of pods are available whereas deployment are reponsible for managing different versions of the application. Like deployemnt replicaset cant rollout or rollback to different version of application nor maintain any revisions for the same.

## Deployemnt Configuration

**Below is the yaml file for Deployment.**

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  namespace: facebook
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
  revisionHistoryLimit: 10
  paused: false
  replicas: 3
  minReadySeconds: 10
  selector:
    matchLabels:
      role: webserver
      jane: akil
    matchExpressions:
      - {key: version, operator: In, values: [v1, v2, v3]}
  template:
    metadata:
      name: web
      labels:
        role: webserver
        version: v3
        tier: frond
        jane: akil
    spec:
      containers:
      - name: web
        image: nginx:1.20-perl
        ports:
        - containerPort: 80
          protocol: TCP
---
apiVersion: v1
kind: Service
metadata:
  name: web-service
  namespace: facebook
  labels:
    role: web-service
spec:
  selector:
    role: webserver
  type: NodePort
  ports:
  - port: 80
    nodePort: 32001
```

**Key elements of above YAML file:**

- We are creating deployment type file Strategy is which means if any changes is there it will apply those changes.
- The RollingUpdate will check if any request is server by the conainer after the request is being served it will aply the changs.
- Rivision history limit means number of changes that can prform it will keep track of all revision in the form of revisions.
- MaxSurge means whenever a revision is applied it will create specified number of container according to the values is given it will apply it to the pod.

