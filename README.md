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

Eg: We can group Shopping Cart and Recomendation engine in same pod if they are going to continuously interact with one another i.e coupled or dependent in some way

**Node** 

A node is a worker machine in Kubernetes - a workload is run by putting containers into pods which run on nodes. A node can be either a virtual or physical machine, depending on the cluster.

**Service**

An abstraction which defines a set of pods and makes sure that network traffic can be directed to the pods for the workload.
We use service to expose application and make it available over network.
Load balancer is am example of service.

**Cluster** 

A cluster is a group of nodes that run  containerised applications. We can manage the cluster and everything it includes with Kubernetes. 
A cluster is made up of a master node and a set of worker nodes. While the control plane works to maintain the desired state of the cluster, the worker nodes actually run the applications and workloads.

**Control plane**

The control plane manages the worker nodes and the Pods in the cluster.


**Namespace**

A virtual ‘slice’ of a cluster where we can provision resources, organise objects and deploy applications inside the cluster.

**Deployment** 

Creating instances if our container. Control plane schedules, monitors and restart instances

**Image** 
  
  The docker image that the deployment will use. Image is a read only template that can create container instances of our application.
  We can store image in container registry (loke Docker Hub, Elastic Container Registry etc)
  
  
### Kubernetes architecture

**Control plane (master)** 

The Control plane is made up of the kube-api server, kube scheduler, cloud-controller-manager and kube-controller-manager. Kube proxies and kubelets live on each node, talking to the API and managing the workload of each node. 
The control plane manages the worker nodes and the Pods in the cluster.

Control plane consists of masters. Kubernetes operates in active passive mode. If a control pane consists of 3 masters, only one is leased and rest of the 2s are followers. Followers proxy all the requests to the leader. If the leader goes down, a new leader is elected.
Kubernetes needs seperate linux machines (physical machine on onprem data center or virtual instance in public cloud) to run each master.

We should run the application in worker nodes and leave to master solely for looking after the cluster

**kube-apiserver**

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane. When we isuue commands to the cluster, we send them to the api server.
It exposes REST API Port an d consumes JSON/YAML.

We send YAML manifest files describing our apps to the api server. It authenticates and validates it and then instruct control pane features  to deploy it.

**kubectl**

The Kubernetes command-line tool, kubectl, allows to run commands against Kubernetes clusters.
We can use kubectl to deploy applications, inspect and manage cluster resources, and view logs etc

![image](https://user-images.githubusercontent.com/29271635/128332251-3c34536c-6267-4697-b21e-daaf05ca4070.png)

![image](https://user-images.githubusercontent.com/29271635/128371278-be715591-99d3-4214-8711-28c1916f74d4.png)


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


### EKS - Elastic Kubernetes Service 

It is a managed service that makes it easy to run Kubernetes on AWS without needing to install or operate our own Kubernetes control pane or worker nodes.
