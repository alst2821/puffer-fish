
Pods
----

Example of a stand-alone pod definition, as YAML::

  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
    labels:
      run: nginx-pod
  spec:
    containers:
    - name: nginx
      image: nginx:1.20.2
      ports:
      - containerPort: 80

`Link to workload -> pods <https://kubernetes.io/docs/concepts/workloads/>`_
        
Commands to run pods::

  $ kubectl apply -f nginx.yaml

  $ kubectl run 
