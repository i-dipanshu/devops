# Basic Terminlogy
- **Bare metal server:** Physical computer server that is used by one consumer only and are not running in shared hardware like `Vm's`.
- **Configuration Management:** Management of software and hardware to mantain a desired state.
- **Monolithic Architecture:** An architecture in which application is single-teired, that is say backend, frontend, databases are all the combined together to form a application.
- **Micro - Services:** A micro-services is an architecture where a software is composed of small independent services that communicate over a well defined API.
- **Service Mesh:** A service mesh is a infrastructure that help to securely communication between services.
- **Orchestration:** Orchestration is the automated configuration, management, and coordination of computer systems, applications, and services.

# Kubernetes 
- An orchestrator

# Architecture

- **Cluster** - It contains the nodes.
- **Node** - Present inside a cluster.
- Two types of nodes: 
- 1. `Control Plane`
  - It controls and manages worker nodes.
  - It consists of different component 
  - **API Servers** - communicates with `kubectl` and the rest of cluster components
  - **ETCD** - It is the database in which api server writes
  - **Control Manager** - It makes sure that desired state is always maintained.
  - **Scheduler** - It schedules a task on the working nodes.
- 2. `Worker Node`
  - It contains of `kubelet`, `kubeproxy`, `pods` and `container runtime`.
  - **kubelet:** - It communicates with api servers and the transmit it to container runtime.
  - **kubeproxy:** - Each pod has different ip address which is managed and stores in kubeproxy.
  - **Container Runtime:** - It starts and stops the container inside the pods.
  - **Pods** - It contains container.

# Steps to a Kubernetes Runtime
- Start the microservices
- Conterize the application
- Put the container inside a pod
- Deploy the pods 
