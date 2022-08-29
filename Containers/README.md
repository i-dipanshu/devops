
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

# start a new container
docker run -d --name nginx nginx

# default is the same that host machine has 
cat /sys/fs/cgroup/memory/memory.limit_in_bytes

# resource allocated to container
docker exec -it nginx  bash
cat /sys/fs/cgroup/memory/memory.limit_in_bytes

```
- Since there is no restriction on usage of memory, a single container could use all the memory. So, we need to fix this and restrict container with memory usage
```bash
# In order to use different cgroup we need to create it
mkdir sys/fs/cgroup/memory/<dipanshu>

# start a container with different memory allocation than default
docker run -d -m 6MB --name nginx nginx

# check the memory allocated
docker exec -it nginx bash
cat system.slice/docker-653e68c52719eff5aa7f6e29f7b17aa2a0a7a2cd6ab6375148e5502021fe121f.scope/memory.limit_in_bytes
```
- We can assign a process to a cgroup by writing the `PID` of the process to `cgroup.procs` file for that cgroups
```bash
# change directory to cgroup created
cd sys/fs/cgroup/<dipanshu>

# write your desired memory allocation to `memory.limit_in_bytes` file
cat memory.limit_in_bytes
echo <memory> > memory.limit_in_bytes
cat memory.limit_in_bytes

# obtaining `PID` and  assigning `PID` to cgroup
docker top nginx
echo <PID> cgroup.procs
cat /proc/<PID>/cgroup | grep memory
```


## Namespaces
- By defining a `Namespaces` we can restrict the resources that are visible to that process
- We can access the namespaces by `lsns` but it can be incomplete because that the whole point of namespaces ie; to create isolation.
- There are different types of namespaces like `UID`, `PID` etc
- `UID` namespaces control the isolation of `hostname and domain name`.
- `PID` are process id that each process have, which creates a isolation as all `PID` are unique.

## UID
- We can change hostname using `unshare` command.
```bash
# to check hostname
hostname

# create a container and check its hostname which will be different as container are isolated
docker run -it --name nginx nginx bash
hostname

# Use unshare command and open sh shell to change the hostname
sudo unshare -uts sh
hostname
hostname <anyname>
hostname
exit 

# but it doesn't effect root hostname
hostname
```