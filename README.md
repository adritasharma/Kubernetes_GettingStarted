# Kubernetes Getting Started

### What are Containers?

Containers are all about portable software.
Technology that allows to run software on a variety of systems, including a developer’s laptop, all the way to a production system.
Containers wrap software in a standardized environment that allows it to run consistently on varied machines.

Modern applications are made up of a bunch of independent microservices running in containers.

Containers are similar to virtual machine but more like a virtual operating environment. It is a standardized unit with everything a software needs to run (eg: code, libraries, runtimes, system tools)


### What is Orchestration?

Container Orchestration refers to processes used to manage containers and to automate the management of containers.
Deploy new code with zero down time.
For example:

• I want to start up a set of five containers in production.

• I could spin up each container manually.

• Or, I could tell an orchestration tool like Kubernetes that I want five containers, and let the tool do it.

### What are Containers Used For?

 **Software Portability** – Running software consistently on different machines.
 
 **Isolation** – Keeping individual pieces of software separate from one another.
 
 **Scaling** – Increasing or decreasing resources allocated to software as needed.
 
 **Automation** – Automating processes to save time and money.
 
 **Efficient Resource Usage** – Containers use resources efficiently, which saves money.

### What is Docker?

- Docker is primarily a container runtime. 
- Container is not a tool or technology. It is  a concept. Docker is the tool to implement that concept.
- It is a piece of software that is designed to implement and support containers.
- Docker allows us to run containers on systems. 
- It also offers a variety of tools for creating and managing containers and container images. 
- It is a Platform to build, ship and run apps
- Containers run on a Docker host.

### What are other Container runtimes?

- Rkt (Pronounced Rocket)
- Containerd

### What is Kubernetes?

- Kubernetes is a container orchestration tool. 
- It allows easy build and manage container infrastructure and automation.
- It has features  like self-healing applications, automated scaling, and easy automated deployments.

### What are other orchestration tools?

- Docker Swarm
- Kubernetes
- Zookeeper
- Marathon Based
- Nomad

- **Cloud Orchestration Solutions**

    Cloud providers such as Amazon Web Services, Microsoft Azure, and Google Cloud Platform also offer built-in container orchestration solutions, including cloud-native Kubernetes implementations! 
    For example: 
    
    - Red Hat OpenShift
    - Amazon Elastic Container Service 
    - Amazon ECS for Kubernetes (EKS)
    - Azure Kubernetes Service 
    - Google Kubernetes Engine


### Kubernetes Terminologies

**Container** 

Software technology that packages an application along with its runtime dependencies.

**Pod** :

The smallest object of the Kubernetes ecosystem, a Pod represents a group of one or more containers running together on your cluster.

A pod share the same IP address space.

Eg: We can group Shopping Cart and Recomendation engine in same pod if they are going to continuously interact with one another i.e coupled or dependent in some way like they need to share volumes, memory etc.

![image](https://user-images.githubusercontent.com/29271635/128674885-c92adb2c-6ba5-4a0a-9e85-db290856253c.png)


**Node** 

A node is a worker machine in Kubernetes - a workload is run by putting containers into pods which run on nodes. A node can be either a virtual or physical machine, depending on the cluster.

**Service**

Service sends traffic to healthy pods. It is an abstraction which defines a set of pods and makes sure that network traffic can be directed to the pods for the workload.
We use service to expose application and make it available over network.
Load balancer is an example of service.

When a pod goes down, a new pod spins with a different IP address. Kubernetes svc manages the netword traffic.

![image](https://user-images.githubusercontent.com/29271635/129694338-d2ae21c8-2c3d-4c63-9b98-dec1554cb7eb.png)


**Cluster** 

A cluster is a group of nodes that run  containerised applications. We can manage the cluster and everything it includes with Kubernetes. 
A cluster is made up of a master node and a set of worker nodes. While the control plane works to maintain the desired state of the cluster, the worker nodes actually run the applications and workloads.

**Control plane**

The control plane manages the worker nodes and the Pods in the cluster.


**Namespace**

A virtual ‘slice’ of a cluster where we can provision resources, organise objects and deploy applications inside the cluster.

**Deployment** 

Creating instances if our container. Control plane schedules, monitors and restart instances.

Deployment Controller/ Reconciliation loop watches API server for new deployments and implements them/
It constantly compares observed state with desired state.

Suppose observed state has 4 replicas. Therefore 4 pods are instantiated. Now 1 pod goes doen, so observed state is 3 and desired state is 4. Deployment Controller works with Replica state and spins a new pod immediately.

The desired state is maintained in the manifest yaml file.

![image](https://user-images.githubusercontent.com/29271635/129708437-3e1a6260-a4b7-4d71-bf1e-83d167e1efb8.png)




**Image** 
  
  The docker image that the deployment will use. Image is a read only template that can create container instances of our application.
  We can store image in container registry (loke Docker Hub, Elastic Container Registry etc)
  
  
## Kubernetes architecture

### Control plane (master) Components 

The Control plane is made up of the kube-api server, kube scheduler, cloud-controller-manager and kube-controller-manager. Kube proxies and kubelets live on each node, talking to the API and managing the workload of each node. 
The control plane manages the worker nodes and the Pods in the cluster.

Control plane consists of masters. Kubernetes operates in active passive mode. If a control pane consists of 3 masters, only one is leased and rest of the 2s are followers. Followers proxy all the requests to the leader. If the leader goes down, a new leader is elected.
Kubernetes needs seperate linux machines (physical machine on onprem data center or virtual instance in public cloud) to run each master.

We should run the application in worker nodes and leave to master solely for looking after the cluster


**Kubernetes API**

Pods, Services, Deployment, replica set, job, cronjob, secrets, nodes etc (everything) are objects in Kubernetes API. The API contains the defination and feature set of each object in Kubernetes.

![image](https://user-images.githubusercontent.com/29271635/129861114-e5f67fd5-016f-49cf-8572-63ba608153fb.png)


**kube-apiserver**

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API over secure Restful endpoints. The API server is the front end for the Kubernetes control plane. When we isuue commands to the cluster, we send them to the api server.
It exposes REST API Port and consumes JSON/YAML.

We send YAML manifest files describing our apps to the api server. It authenticates and validates it and then instruct control pane features  to deploy it.

**etcd**

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

**kube-controller-manager**

It is the Control plane component that runs controller processes.

Each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.

Some types of these controllers are:

- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
- Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.
- Deployment controller


**kube-scheduler**

It watches  API server for new work tasks and assigns work to cluster nodes.


**kubectl**

The Kubernetes command-line tool, kubectl, allows to run commands against Kubernetes clusters.
We can use kubectl to deploy applications, inspect and manage cluster resources, and view logs etc

![image](https://user-images.githubusercontent.com/29271635/128332251-3c34536c-6267-4697-b21e-daaf05ca4070.png)

![image](https://user-images.githubusercontent.com/29271635/128371278-be715591-99d3-4214-8711-28c1916f74d4.png)

### Node Components 

**kubelet**

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. It watches API server for new work tasks (Pods).
It reports back to Masters

Nodes can be linux or Windows machines.

**Container runtime**

It can be docker. It is pluggable to Container runtime Interface (CRI),

**kube-proxy**

kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

Each pod has a single IP


## Workflow

App Code (with Docker File) **->** Build Container Image **->** Store Image in Registry (eg: Docker Hub) **->** Define K8 Manifest(yaml) files **->** POST in API Server

### Creating Pod Manifest 

**pod.yml**
```
# Simple Kubernetes Pod to deploy the app contained in adritasharma/getting-started-k8s:1.0

apiVersion: v1 
kind: Pod
metadata:
  name: hello-pod
  labels:
    app: web
spec:
  containers:
    - name: web-ctr
      image: adritasharma/getting-started-k8s:1.0
      ports:
        - containerPort: 8080
```


### Deploying Pod

We can deploy the Pod in any Kubernetes Cluster (ex: Docker Desktop, AKS, GKE etc).

`kubectl apply -f pod.yml`

In this command, kubectl will POST the file to the API server. It will authenticate and assign the pod to a node

To view the pods:
 
`kubectl get pods`

![image](https://user-images.githubusercontent.com/29271635/130047593-e81a81b9-555f-464f-8329-629ccaef573f.png)

Note: Nodes are Virtual machines or cloud instances, pods are applications. Pods run in the node.


## Kubernetes Service


Kubernetes Service Object expose application internally and externally, i.e within the cluster (eg- from another pod running in the same cluster) and to the outside world.

There are mainly 3 types of service

- **ClusterIP** (default) - It only makes the IP available inside the cluster
- **NodePort** - External access via nodes
- **LoadBalancer** - External access via cloud load-balancer


![image](https://user-images.githubusercontent.com/29271635/130635459-f070863d-a638-4a4a-b536-94ab2309026b.png)


We can see a Pod,'s IPs when we run `kubectl get pods` but these IPs are not reliable as a Pod may go down. Service sends traffic to the helthy pods
Pods IP.

Service object is a REST object in Kubernetes API

![image](https://user-images.githubusercontent.com/29271635/130634700-2bc3a546-e1d0-4b62-a7ef-a303e858a385.png)


### Connecting Service with Pods.

Pod manifest contains a label. If we add this label name to the service selector, then the service is going to send traffic to that Pod.

![image](https://user-images.githubusercontent.com/29271635/130636207-48bf4028-2681-4d44-9ae6-5ea0f1b12154.png)

**Node Port**

It is the option to create port for the service on every cluster node. Node Port also creates a Cluster IP

![image](https://user-images.githubusercontent.com/29271635/130639939-717372f1-c992-442d-887d-4d5d7e3caa76.png)

### Creating Service Imperatively

It is Imperative way because `kubectl expose` is the command to create the service and then all the config options are listet here in the command line. We aare not pulling them from config file that we can store in a code repository that can be versioned

`kubectl expose pod hello-pod --name=hello-svc --targer-port=8080 --type=NodePort`

Note: hello-svc will be registered in DNS

`kubectl get svc`

![image](https://user-images.githubusercontent.com/29271635/130787613-6b2f9c6b-6d03-4393-b98c-614fbb89e409.png)



### Creating Service Declaratively

![image](https://user-images.githubusercontent.com/29271635/130787913-f21d3b18-c904-4175-92d2-9a775c0d0087.png)

Note: ps-nodeport will be registered in DNS


### Creating LoadBalancer Services

It only works with Cloud that supports Load Balancer

![image](https://user-images.githubusercontent.com/29271635/130815610-aa1cc564-fcba-43b9-87d0-c09056dbcda8.png)


`kubectl apply -f svc-lb.yml`

`kubectl get svc`

![image](https://user-images.githubusercontent.com/29271635/130815815-3fc5010c-86aa-4a74-b9df-58a7da0cc92e.png)

# Kubernetes Deployment

Kubernetes Deployment is an object in Kubernetes API in the apps API sub group.


It has this important features:

- Self Healing
- Scaling
- Rolling Updates
- Rollbacks

![image](https://user-images.githubusercontent.com/29271635/130995163-3658e92a-4d4b-4614-be36-10e9e62221a3.png)


### Replica set

Replica set is a API object. It does the Self healing and scaling. It continously monitors observed and desired state.

## Creating Deployment YAML

```
# Simple deployment used to deploy and manage the app in nigelpoulton/getting-started-k8s:1.0

------------------- Deployment Spec -------------------------------------------- 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deploy
  labels:
    app: web
spec:
  replicas: 5
  selector:
    matchLabels:
      app: web
------------------- Pod Spec --------------------------------------------      
  template:
    metadata:
      labels:
        app: web
    spec: 
      terminationGracePeriodSeconds: 1
      
------------------ Container Spec  (<app>) -------------------------------
      containers:
      - name: hello-pod
        image: nigelpoulton/getting-started-k8s:1.0
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
```

- Here since Replica is 5, 5 pods will be running the same application.
- The deployment must know which Pods it is managing (updates, rollbacks etc). The label selector in deployment spec must match the label selector in Pod spec. 

### Deploying

`kubectl apply -f deploy.yml`

`kubectl get pods -- show-labels`

![image](https://user-images.githubusercontent.com/29271635/131467873-50c33553-4dd7-4faf-8510-35c465c738a8.png)


`kubectl get deploy`

![image](https://user-images.githubusercontent.com/29271635/131466612-98b37649-5078-4701-aa82-8fd52dd3cff1.png)

`kubectl get rs`

![image](https://user-images.githubusercontent.com/29271635/131466677-f6e1d3c9-1a9d-4c42-9f0e-515833c339f1.png)

`kubectl describe svc ps-lb`

![image](https://user-images.githubusercontent.com/29271635/131467108-b648ea05-cab7-4049-b6d1-cfc2e2d6ff92.png)


The load balancer service was running long before the new pods were added. It has selector label - app=**web** and the new pods also have the same label **web**. Labels are dynamic. The service by watching the API server saw new pods arrive and added them to the healthy endpoints.

`kubectl describe ep ps-lb`

![image](https://user-images.githubusercontent.com/29271635/131468198-831fc1b5-90f2-4281-93b6-15cdd33b311a.png)

The Addresses are the IPs of our 5 Replicas

### Self Healing

We will delete a Pod

![image](https://user-images.githubusercontent.com/29271635/131469312-97e955b5-10ac-4c6f-b730-715759959b46.png)

We will get the Pod list again

`kubectl get pods`

![image](https://user-images.githubusercontent.com/29271635/131469414-2dcecc96-e40c-414c-9255-fc28acdcd246.png)

We can see that there are 5 Pods even after we deleted 1.  One of the Pod's age is just 10s. This means this Pod was created just after we deleted 1 pod and thus maintaing 
sesired state and current state

### Scaling

We increase the replicas in deployment.yml

![image](https://user-images.githubusercontent.com/29271635/131470196-d21445cc-ec4f-4760-96f9-9cc423e774fa.png)

`kubectl apply -f deploy.yml`

`kubectl get pods`

![image](https://user-images.githubusercontent.com/29271635/131470330-ad5494d6-9663-4378-8434-86e565dbee28.png)


### Rolling Updates

------------------- Deployment Spec -------------------------------------------- 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deploy
  labels:
    app: web
spec:
  selector:
    matchLabels:
      app: web
  replicas: 10
  minReadySeconds: 5
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 0
      maxSurge: 1
```

- **RollingUpdate strategy** means anytime we update the image (in the Container Spec of Deployment.yml), instead of deleting all the existing pods, and replacing them all in 1 go with 10 new ones, it should create 1 new pod and terminate 1 old one in a repeated cycle (here 10 times)

- **maxUnavailable**: 0 - Always maintain 10 pods
- **maxSurge**: 1 - During an update we can surge 1 pod more than the desired state i.e upto 11 Pods
- **minReadySeconds**: 5 - The new pod should be up and running for min 5 seconds before an old one is terminated

So Kubernetes will deploy 1 new pod on the new version (the 11th Pod), wait until it is up and running for minimum 5 seconds then terminate an old Pod. It will repeat the process until it cycles through all 10 Pods

### Rollbacks

Old replica set from old Pod versions stays in the cluster which makes it easy for rollbacks.

`kubectl get rs`

![image](https://user-images.githubusercontent.com/29271635/131511770-fc26ed5d-fc31-47e5-9414-e61c8169234a.png)


- The 1st one manages the new replicas.
- The second one manages the old replicas. Even if it doesn't have any Pods now, it is still present in the cluster

**Rollback**

`kubectl rollout undo deploy web-deploy --to-revision=1`

![image](https://user-images.githubusercontent.com/29271635/131512462-370cb6bd-888d-41ca-a889-54d99ecd14a8.png)


The Pods are being replaced with the older version 1 at a time following RollingUpdate strategy.

`kubectl get rs`

![image](https://user-images.githubusercontent.com/29271635/131512811-f9ddf88c-2a84-43ab-a0b9-d4a866f949eb.png)
