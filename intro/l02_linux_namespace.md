https://en.wikipedia.org/wiki/Linux_namespaces

namespace limits ability to see a resource

User / IPC / UTS / MOUNT / PID / Network

example: by default adding mount point changes global configuration
by using a namespace, mount points can be assigned to individual container

IPC - communication between processed - namespace could limit communication within container

host names - identify container with  its own host name, giving abi;ity to use standard
tools on a container

network - each container has own network stack (routing tables, e.t.c)

