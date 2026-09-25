# RouteX

RouteX is a high-performance distributed routing and packet processing system with a distributed control plane and a userspace packet-processing data plane.

The control plane is written in Go and manages routing configuration, cluster state, and node health.

The data plane is written in C++ and uses DPDK for high-speed userspace packet processing, with IPv4 LPM for route lookup.

The control and data planes are separated and communicate through gRPC over a Unix domain socket.

```text
                    RouteX
                       |
          +------------+------------+
          |                         |
          v                         v
     control plane             data plane
          go                        c++
          |                         |
    cluster state                 dpdk
    route state                   lpm
    health checks                 packet io
          |                         |
          +---------- grpc ----------+
                    unix socket

Route updates are built and validated as a new routing configuration before being published to the data plane. This allows packet-processing workers to continue operating with a consistent configuration while route changes are applied.

Tech stack
Go
C++
DPDK
gRPC
Unix domain sockets
IPv4 LPM

Status
Initial repository setup.
