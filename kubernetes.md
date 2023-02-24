# Kubernetes

If a container goes down, another container needs to start. That's how Kubernetes comes to the rescue!

Kubernetes features:

- **Service discovery and load balancing:** Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
- **Storage orchestration** Kubernetes allows storage system of our choice, such as local storages, public cloud providers etc.
- **Automated rollouts and rollbacks / Secret and configuration management** like OAuth ssh keys etc.
- We can tell Kubernetes how much CPU and memory (RAM) each container needs.
- **Self-healing:** Kubernetes restarts containers that fail, replaces containers, kills container, heals them

What K8s doesn’t do:

- Does not deploy source code and does not build your application ci/cd
- Does not provide logging, monitoring, or alerting solutions.

---

# Kubernetes Components

![Cluster-node-pods-appl](https://user-images.githubusercontent.com/69111235/221276719-e0480c9d-3a36-4806-9224-f167b4d156a5.png)

node: it is a working machine(physical or virtual)

![components-of-kubernetes](https://user-images.githubusercontent.com/69111235/221276769-1353b790-0bbb-4b43-a5bf-24ffc9f301a8.svg)

| Control Plane (prev master node) | Worker Nodes |
| --- | --- |
| Control Manager (and cloud control manager optional)  | kubelet |
| api server | kubeproxy |
| scheduler | container runtime |
| etcd |   |

**etcd**: is designed to reliably store infrequently updated data in a persistent key-store value store. The key-value store is immutable but creates new structure for new data.

**kube-apiserver**: it exposes k8s api, and its main implementation is to scale horizontally, i.e many instances can be created for loadbalancing

<aside>
💡 The Kubernetes API lets you query and manipulate the state of API objects in Kubernetes (for example: Pods, Namespaces, ConfigMaps, and Events).

</aside>

**scheduler**: kube-scheduler watches for any free/unassigned pods and allocate them to a node. its task is to assign new objects

**controller manager**: it runs controller processes, they are in constant loop-check of the state of cluster

**kubeproxy:** maintains network rules of nodes, each node has its own kubeproxy. responsible for tcp, udp streaming

**kubelet:** it makes sure that containers are running in pods and communicates with contoller plane, runs on each node

<aside>
💡 container runtimes: are the software on which containers run. Kubernetes support. CRI: Shims are Container Runtime Interface (CRI) implementations, interfaces or adapters, specific to each container runtime supported by Kubernetes. eg: cri-o, dockershim(deprecated), containerd-cri.

</aside>

---

# Kubernetes Objects:

k8s objects are persistent entities like deployments, pods, nodes etc that are used to represent the state of cluster like which containerised app are running, resources available, policies available.

<aside>
💡 use `kubectl api-resources` to get list of all objects of k8s

</aside>

k8s objects can be represented in .yaml format

once you create the object, the Kubernetes system will constantly work to ensure that object exists.

To work with objects we use k8s api

Every object field has 2 specifications: spec and status:

- spec: it must be declared to describe fields like name, replicas, desired state etc
- status: it describes current state of object

```yaml
#deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

fields required to create an object:

- apiVersion: version of k8s api
- kind: what kind of object you want to create
- metadata: which helps uniquely identify the object
- spec: state of your object

<aside>
💡 difference between objects and resources:      [https://stackoverflow.com/questions/52309496/difference-between-kubernetes-objects-and-resources](https://stackoverflow.com/questions/52309496/difference-between-kubernetes-objects-and-resources)                                                                                              Objects are entities which are a representation of version+kind+group. eg: api v1 pod. Resource is a specified URL to obtain an object from a group of API objects. eg: api/v1/pods

</aside>

A collection of objects of a certain kind form an API resource

---

# Kubernetes Resource

In Kubernetes, a resource is an object that can be created, updated, and deleted in a cluster.

Example: 

- pods
- services
- namespaces
- replication controllers
- controllers like /
1. statefulsets
2. daemonsets
- persistent volumes
- cronjobs
- ingress
- config maps
- secrets

---

# Custom Resource Definitions CRDs

A custom resource definition (CRD) defines a CR and lists out all of the configuration available to users of the operator 

A *custom resource definition*
 (CRD) file defines your own object kinds and lets the API Server handle the entire lifecycle

When we create a CRD the Kubernetes API Server creates a RESTful API path for each version.

eg: for filename `resourcedefinition.yaml`

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
# name must match the spec fields below, and be in the form: <plural>.<group>name: crontabs.stable.example.com
spec:
# group name to use for REST API: /apis/<group>/<version>group: stable.example.com
# list of versions supported by this CustomResourceDefinitionversions:
    -name: v1
# Each version can be enabled/disabled by Served flag.served:true# One and only one version must be marked as the storage version.storage:trueschema:
openAPIV3Schema:
type: object
properties:
spec:
type: object
properties:
cronSpec:
type: string
image:
type: string
replicas:
type: integer
# either Namespaced or Clusterscope: Namespaced
names:
# plural name to be used in the URL: /apis/<group>/<version>/<plural>plural: crontabs
# singular name to be used as an alias on the CLI and for displaysingular: crontab
# kind is normally the CamelCased singular type. Your resource manifests use this.kind: CronTab
# shortNames allow shorter string to match your resource on the CLIshortNames:
    - ct
```

to create the CRD: `kubectl apply -f resourcedefinition.yaml`

this endpoint is created:

`/apis/stable.example.com/v1/namespaces/*/crontabs/...`

Now this endpoint is used to manage and create Custom Objects

# Custom Resources

A *custom resource*
 is an object that extends the Kubernetes API or allows you to introduce your own API into a project or a cluster.

these are custom resources that we can build which are not provided by kubernetes by default.

for eg: CronTab is the Custom Resource from the above CRD.

# Custom Objects

We can create instances of our Custom Resources  by creating Custom Objects.

Eg: for filename: `my-crontab.yaml`

```yaml
apiVersion: "stable.example.com/v1"
kind: CronTab
metadata:
name: cronobj1
spec:
cronSpec: "* * * * */5"
image: my-awesome-cron-image
```

to create Custom Object: `kubectl apply -f my-crontab.yaml`

Here the Custom Object `cronobj1` is created. We can create more than one Custom Object instances from our CRDs.

---

# Controllers vs Operators

| controllers | operators |
| --- | --- |
| Controllers are used to watch and manage the state of cluster and take action to bring them to desired state | Operators |
| they are in constant loop to check cluster’s state | built on top of operators? |
| eg: daemonset, statefulsets | eg: prometheus rule |
| It’s a controller’s job to ensure that, for any given object, the actual state of the world |  |

<aside>
💡 for exact meaning of difference b/w operators and controllers see this comment: [https://github.com/kubeflow/training-operator/issues/300#issuecomment-357319596](https://github.com/kubeflow/training-operator/issues/300#issuecomment-357319596)

</aside>

A Kubernetes operator is a method of packaging, deploying, and managing a Kubernetes application using custom resources. A Kubernetes application is both deployed on Kubernetes
 and managed using the Kubernetes API

---

> Let's start with understanding what CRDs are. In general, when you start a k8s cluster you can do `kubectl get pods or deployments or secrets`
> 
> 
> The K8s cluster runs an API server which knows what these resources are and it replies stating the respective resources which are in the cluster. For ex, it will list the pods or secrets etc. Now as k8s started getting adopted more, people wanted to create their own resources. Similar to a "Deployment", they wanted to have a resource named say "Job", or "Memcached". Now these resources are not known by the API server. These are called custom resources. To inform API server of what these resources are and what they look like we have CRDs - Custom Resource Definition.Now a controller is nothing but a state machine. It tries to reconcile your current state so that it eventually reaches the desired state. As soon as it sees a difference between the current and desired state it takes an action to reconcile. Controllers perform these 3 important things - watch, check for diff, reconcile (take some action).Operators are built on top of controllers. They do the same thing as a controller does but for custom resources. And the "action/reconcile" step which we were talking about in the previous paragraph, is customizable application specific logic in an operator. An operator can watch a custom resource, check if its state is different from the desired state, and reconcile according to a logic which is application specific written by a developer. In short, they follow the same controller pattern.
> 

---
