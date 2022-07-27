# Deployements before Kubernetes
**Before starting what is kubernetes and lets understand how deployements were taking place before Kubernets.**

we were having three kinds of deployemets : 
- Traditional deployements.
- Vitualized Deployements.
- Container Deployemnts.

![image](https://user-images.githubusercontent.com/69069614/180745350-18e3b73e-c0b4-4be0-85af-46fdd2ff0f2e.png)

1. In the **Traditional deployements** we have our server/machine on which we were installing our OS and on that OS we are running our application. But what if you want to expand your business and also user base is also increasing which requires your application to be upgraded what we will you do ? you will install more servers which will cost you more, their maintainence, resource consumption will also increase etc. Then we moved to another kind of deployements which is Virtualized Deployements.

2. In **Virtualized Deployements** we have the same setup with that we have one hypervisor on which we can run multiple os and on top of that we can run our application and also if we want to sacle up we can install multiple OS but we have limitation with that also as those guest OS will consume your machine resources which will be slow at some point and cant serve high requests. Then we move to another kind of deployeements which is container deployements.

3. In **Container Deployements** we have same setup with conatiner runtime engine on which OS will be running in the form libararies and on top of that os we are running our application with containerization its become easy deploy our application as it spins up faster and as well as requires less resources.

# Why We Need Kuberenets ?

In docker we maintain containers on the machines but **what if machines gets crashed then we are no able to access that container**. Here is the role of Kubernetes. Kubernetes forms a cluster in which it has several machines connected and on top of that cluster the containers are used. The advantage of this is if any machines goes down there will be other machines which serve container.

# What is Kuberentes ?
In general Kubernetes is a open source platform and container orchestration tool for automating deployment, scaling and operations of application containers.
it follows the concept of Master and worker nodes cluster which are highly available without any downtime or we can say very minimum amount of downtime.

# Architecture of Kubernetes.
As we all know There is Master node and Worker node but how this cluster works. There are several components lets see one by one : 


![k8_architecture-removebg-preview](https://user-images.githubusercontent.com/69069614/181056970-cece8ac9-4597-45b9-b447-e2f90f8ddd67.png)

**Kubernetes Componenets**

**1. API Server**

It is use to communicate with other componenets of different or within server. If server wants to comunicatewith other componenets it will be done via API server these should be exposed to HTTPD. Instead of communicating through port e can easily communicate via API.

**2. ETCD**

ETCD stores the configuration information which can be used by each node in the cluster. ETCD is Consistent and highly-available and store the data into key value format used as Kubernetes' backing store for all cluster data and It stores all the data used to manage the cluster. It is accessable only by Kubernetes API server. 

**3. Controller Manager**

Controller Manager is responsible for all the activities in the cluster whatever changes that has to be done that will be approved by controller manager. Before doing any changes it wil check the old configuration in th ETCD then it will approve the chnages and will commit those changes in the ETCD as well and id the changes are not executed properly then it will not commit those in the ETCD.

There are Different Controller in the conrol pane each one has seperate Process. They are all compiled in a single binary and working in a single process
Some types of controller are :

- **Node Controller :** It is mainly responsible for noticing and responding when any of the nodes goes down.
- **Job Controller :** It is responsible for creating pods to run the tasks so that it can be completed. it keep on watches for the job and creates the pod for the same.
- **Endpoint Controller :** It is reponsible for provisionng the endpoints such as service endpoits,pods etc.
- **Service Account & Token controllers :** It is responsible for creating defaults services account, API token access for namespaces.

**4. Scheduler**
