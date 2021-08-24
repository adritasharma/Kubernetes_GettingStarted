# Kubernetes Getting Started

### What are Containers?

Containers are all about portable software.
Technology that allows to run software on a variety of systems, including a developer’s laptop, all the way to a production system.
Containers wrap software in a standardized environment that allows it to run consistently on varied machines.

Modern applications are made up ofa bunch of independent microservices running in containers.

Containers are similar to vairtual machie but more like a virtual operating environment. It is a standardized unit with everything a software needs to run (eg: code, libraries, runtimes, system tools)


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

![image](https://user-images.githubusercontent.com/29271635/130635459-f070863d-a638-4a4a-b536-94ab2309026b.png)

We can see a Pod,'s IPs when we run `kubectl get pods` but these IPs are not reliable as a Pod may go down. Service sends traffic to the helthy pods
Pods IP.

Service object is a REST object in Kubernetes API

![image](https://user-images.githubusercontent.com/29271635/130634700-2bc3a546-e1d0-4b62-a7ef-a303e858a385.png)


### Connecting Service with Pods.

Pod manifest contains a label. If we add this label name to the service selector, then the service is going to send traffic to that Pod.

![image](https://user-images.githubusercontent.com/29271635/130636207-48bf4028-2681-4d44-9ae6-5ea0f1b12154.png)

