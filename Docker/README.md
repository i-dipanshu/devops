
## Virtual Machine 
- `Virtual Machine` are build on top of a host Machine by a `Hypervisor` and runs in isolation from the host machine.
-  It uses its own `OS`and allocated resources.
-  `Hypervisor` controls and manages multiple `VM` on a host machine.
-  `Hypervisor` are of two types : `Type 2 Hypervisor` or `Hyper-V`.
- `Type 2 Hypervisor` can be installed over host operating system and used to create a virtual machine.

- `Hyper-V` removes the `os layer` , mostly used on servers


## Why Containers ??
- In today world, technology is changing so fast. Like a `node.js` application build 2 months ago has different `dependencies` than one build today , some are deprecated and some are not supported anymore.
- So, when it comes to sharing an application or deploying, it was tough get the application running on various machine as those have different `runtime` than ours.
- This was not the only problem, `VM` takes a significant amount of resources but what if it needs very little than provided. This caused some % of resources unused.
- Scaling of the application was not easy task and many more problem ...

## Containers
- `Containers` are like Virtual Machine but it runs on the same os.
- In more basic context, It just like container in real world, ie; it creates a isolation from rest of the machine using different technology like `PID, UID, Namespaces` and runs on its own.
- A container has everything it needs to run an application from operating system to every dependencies and to create the same runtime environment in it was build. This makes sure that application will 100% of time.
- Basically, containers are just `isolation of some resources on machine`


## Docker and its Architecture
- Docker is `container platform` which has major role in making the container what is it today.
- It helps us to manage and control a container.
## cgroup
- **cgroup:** kernel features which allows allocates resources to different collection of processes
```bash
# list the cgroups on a machine
ls /sys/fs/cgroups

# memory cgroups - this is default for allocation for resources
ls /sys/fs/cgroup/memory

# to use different cgroup we first need to build it
mkdir /sys/fs/cgroup/memory/<newcgroup>

#

```
