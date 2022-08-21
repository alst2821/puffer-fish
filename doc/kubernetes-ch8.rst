=============================
kubernetes course, chapter #8
=============================

kubernetes object types:
  
  - nodes
  - namespaces
  - pods
  - replicasets
  - deplayments
  - daemonsets
          
There is the `spec` section that the cluster tries to match with
a `status`.

Types of nodes:

  - control plane and
  - worker node.

Control plane agents:

  - api server
  - scheduler
  - controller managers
  - etcd
  - kubelet
  - kube-proxy
  - container runtime
  - possible addons
    - container networking
    - monitoring
    - logging
    - dns
    - etc.

Node agents:

  - kubelet and
  - kube-proxy
  - possible addons
    - container networking
    - monitoring
    - logging
    - dns
    - etc.
  
Namespaces is a `killer` kubernetes feature.
There are these namespaces generally::

  % kubectl get namespaces
  NAME                   STATUS   AGE
  default                Active   5d17h
  kube-node-lease        Active   5d17h
  kube-public            Active   5d17h
  kube-system            Active   5d17h



