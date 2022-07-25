# Deployements before Kubernetes
**Before starting what is kubernetes and lets understand how deployements were taking place before Kubernets.**

we were having three kinds of deployemets : 
- Traditional deployements.
- Vitualized Deployements.
- Container Deployemnts.

![image](https://user-images.githubusercontent.com/69069614/180745350-18e3b73e-c0b4-4be0-85af-46fdd2ff0f2e.png)

1. In the **Traditional deployements** we have our server/machine on which we were installing our OS and on that OS we are running our application. But what if you want to expand your business and also user base is also increasing which requires your application to be upgraded what we will you do ? you will install more servers which will cost you more, their maintainence, resource consumption will also increase etc. Then we moved to another kind of deployements which is Virtualized Deployements.

2. In **Virtualized Deployements** we have the same setup with that we have one hypervisor on which we can run multiple os and on top of that we can run our application and also if we want to sacle up we can install multiple OS but we have limitation with that also as those guest OS will consume your machine resources which will be slow at some point and cant serve high requests. Then we have another
