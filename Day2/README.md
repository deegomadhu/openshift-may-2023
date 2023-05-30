# Day2

## What is Container Orchestration Tool/Platform?
- helps us manage containerized applications
- high availability
- supports inbuilt monitoring tools/features
- cluster based tool
- cluster has more than one server/virtual machine spread across cross-geo location
- cluster is a group of servers
- OpenShift recommends to setup atleast 3 master nodes and 2 or more worker nodes
- supports scaling up/down your application based certain rules
- For instance, if the user-traffic to your application increases, you may scale up( add more instances of your applications )
- For instance, if the user-traffic to your application decreases, you may scale down( remove some idle application instances )
- Rolling update
  - is a feature that supports upgrading your live application from one version to another without any down time
  - also supports rolling back to old version if latest version is found to be buggy/unstable
  - you can check how many differt revisions of your application is available in the container orchestration platform cluster
  - it also supports exposing your applications via a service abstraction
  - it supports service discovery
  - comes with in-built load balancers
  - supports 2 types of services
    1. Internal service
       - are accessible only within the container orchestration cluster
       - example
         - ClusterIP Service
    2. External service
       - are accessible outside the container orchestration cluster as well
       - example
         - NodePort Service
         - LoadBalancer Service
  - OpenShift also supports a new feature called route which provides a friendly URL similar to Kubernetes Ingress that helps you access the service outside the cluster network( or from Internet/LAN, etc.,)
Examples
1. Docker SWARM
2. Google Kubernetes
3. Red Hat OpenShift

## Docker SWARM
- a container orchestration platform from Docker Inc organization
- it only supports Docker containers

## Google Kubernetes
- it is opensource
- production grade
- container orchestration platform from Google
- developed in Go Programming language
- supports many different types of Containers including Docker

## Red Hat OpenShift
- is is production grade Enterprise product from Red Hat
- it is developed on top of Google Kubernetes
- supports many additional features in addition to what Google Kubernetes supports
- For example
  - User administration is supported in OpenShift but not Kubernetes
  - Supports Private Container Registry out of the box unlike Kubernetes
  - Supports something called route ( public url) to access the external services
- Latest version even support scaling up/down nodes(virtual machines)

## Kubernetes tools
1. kubectl - client tool with which we would interacting with the Kubernetes cluster
2. kube-admin - administration tool used to create/destroy cluster, add new nodes, remove nodes from cluster,etc
3. kubelet - runs a service, this is the component which actually deploys user-application on the machine where kubelet is running, monitors the health of user-application, reports periodically to API Server about the status of every application running on a particular node

## OpenShift tools
- oc - is similar to kubectl in Kubernetes
- also supports kubectl 

## Kubernetes/OpenShift Resources
- Pod 
  - is a group of related containers
  - the smallest unit that can be deployed 
  - Pod contains one or more application containers, recommended practice is one Pod should represent a single application
  - managed by ReplicaSet
  
- ReplicaSet
  - managed by Deployment
  - supports scale up/down
  - represents a group of Pods of same type
  - monitors health of Pods
 
- Deployment
  - this represents an application
  - this tells what container image should be used to deploy your application
  - this tells how many instances should be created
  - health/liveliness if any
  - each Deployment has one or more ReplicaSet
  - Deployment supports Rolling update
  - Deployment monitors the health of Replicaset

## What is API Server
- is the Core component of Kubernetes/Openshift
- supports REST API for everything in Kubernetes/OpenShift
- all the K8s components only communicate to API Server
- API Server doesn't directly talk to other components, instead it broadcasts events
- Controllers normally register to certain events and act on specific resources based on the events received

## etcd database
- this database is used only by API Server
- key/value pair database
- this holds the entire cluster status and application status

## Scheduler
- this is the components that is reponsible to identify a healthy node/server where any application Pods can deployed
- Scheduler just identifies a nodes and sends the scheduling recommendations to API Server via REST Call

## Controller Managers
- this is a groupd Controllers
- Example
  - Deployment Controller is responsible for managing your application Deployments

# Red Hat OpenShift commands

## Listing openshift cluster nodes
```
oc get nodes
kubectl get nodes
```

Expected output
<pre>
jegan@tektutor:~/openshift-may-2023$ <b>oc get nodes</b>
NAME                             STATUS   ROLES                         AGE     VERSION
master-1.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h52m   v1.26.3+b404935
master-2.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h51m   v1.26.3+b404935
master-3.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h51m   v1.26.3+b404935
worker-1.ocp4.tektutor.org.ocp   Ready    worker                        5h27m   v1.26.3+b404935
worker-2.ocp4.tektutor.org.ocp   Ready    worker                        5h27m   v1.26.3+b404935

jegan@tektutor:~/openshift-may-2023$ <b>kubectl get nodes</b>
NAME                             STATUS   ROLES                         AGE     VERSION
master-1.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h52m   v1.26.3+b404935
master-2.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h52m   v1.26.3+b404935
master-3.ocp4.tektutor.org.ocp   Ready    control-plane,master,worker   5h52m   v1.26.3+b404935
worker-1.ocp4.tektutor.org.ocp   Ready    worker                        5h27m   v1.26.3+b404935
worker-2.ocp4.tektutor.org.ocp   Ready    worker                        5h27m   v1.26.3+b404935
</pre>
