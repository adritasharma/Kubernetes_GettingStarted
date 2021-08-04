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

**Node** 

A node is a worker machine in Kubernetes - a workload is run by putting containers into pods which run on nodes. A node can be either a virtual or physical machine, depending on the cluster.

**Cluster** 

A cluster is a group of nodes that run  containerised applications. We can manage the cluster and everything it includes with Kubernetes. 
A cluster is made up of a master node and a set of worker nodes. While the control plane works to maintain the desired state of the cluster, the worker nodes actually run the applications and workloads.

**Control plane**

The control plane manages the worker nodes and the Pods in the cluster.


**Namespace**

A virtual ‘slice’ of a cluster where we can provision resources, organise objects and deploy applications inside the cluster.

control plane in Kubernetes?
The control plane manages the worker nodes and the Pods in the cluster.

**Deployment** 

Creating instances if our container. Control plane schedules, monitors and restart instances
  
### EKS - Elastic Kubernetes Service 

It is a managed service that makes it easy to run Kubernetes on AWS without needing to install or operate our own Kubernetes control pane or worker nodes.
