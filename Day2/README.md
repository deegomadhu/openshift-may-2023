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

## Finding more details about a node
```
oc describe node master-1.ocp4.tektutor.org.ocp
```

Expected output
<pre>
jegan@tektutor:~/openshift-may-2023$ <b>oc describe node master-1.ocp4.tektutor.org.ocp</b>
Name:               master-1.ocp4.tektutor.org.ocp
Roles:              control-plane,master,worker
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=master-1.ocp4.tektutor.org.ocp
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node-role.kubernetes.io/master=
                    node-role.kubernetes.io/worker=
                    node.openshift.io/os_id=rhcos
Annotations:        machineconfiguration.openshift.io/controlPlaneTopology: HighlyAvailable
                    machineconfiguration.openshift.io/currentConfig: rendered-master-88de65d4c0fd6d1d4d4ef45a11b3c0f9
                    machineconfiguration.openshift.io/desiredConfig: rendered-master-88de65d4c0fd6d1d4d4ef45a11b3c0f9
                    machineconfiguration.openshift.io/desiredDrain: uncordon-rendered-master-88de65d4c0fd6d1d4d4ef45a11b3c0f9
                    machineconfiguration.openshift.io/lastAppliedDrain: uncordon-rendered-master-88de65d4c0fd6d1d4d4ef45a11b3c0f9
                    machineconfiguration.openshift.io/lastSyncedControllerConfigResourceVersion: 21062
                    machineconfiguration.openshift.io/reason: 
                    machineconfiguration.openshift.io/state: Done
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 30 May 2023 06:21:27 +0530
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  master-1.ocp4.tektutor.org.ocp
  AcquireTime:     <unset>
  RenewTime:       Tue, 30 May 2023 12:44:19 +0530
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Tue, 30 May 2023 12:43:08 +0530   Tue, 30 May 2023 06:21:27 +0530   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Tue, 30 May 2023 12:43:08 +0530   Tue, 30 May 2023 06:21:27 +0530   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Tue, 30 May 2023 12:43:08 +0530   Tue, 30 May 2023 06:21:27 +0530   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Tue, 30 May 2023 12:43:08 +0530   Tue, 30 May 2023 06:26:02 +0530   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  192.168.122.209
  Hostname:    master-1.ocp4.tektutor.org.ocp
Capacity:
  cpu:                4
  ephemeral-storage:  104266732Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             15992568Ki
  pods:               250
Allocatable:
  cpu:                3500m
  ephemeral-storage:  95018478229
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             14841592Ki
  pods:               250
System Info:
  Machine ID:                                  526deb693bbe47d4b77c7a65a75a7a2a
  System UUID:                                 526deb69-3bbe-47d4-b77c-7a65a75a7a2a
  Boot ID:                                     09e0086e-8da1-4028-9214-5451a2b9796f
  Kernel Version:                              5.14.0-284.13.1.el9_2.x86_64
  OS Image:                                    Red Hat Enterprise Linux CoreOS 413.92.202305041429-0 (Plow)
  Operating System:                            linux
  Architecture:                                amd64
  Container Runtime Version:                   cri-o://1.26.3-3.rhaos4.13.git641290e.el9
  Kubelet Version:                             v1.26.3+b404935
  Kube-Proxy Version:                          v1.26.3+b404935
Non-terminated Pods:                           (41 in total)
  Namespace                                    Name                                                             CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                                    ----                                                             ------------  ----------  ---------------  -------------  ---
  openshift-apiserver                          apiserver-79458658c8-hws6k                                       110m (3%)     0 (0%)      250Mi (1%)       0 (0%)         5h58m
  openshift-authentication                     oauth-openshift-579b88bdff-dcj2n                                 10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h
  openshift-cloud-controller-manager-operator  cluster-cloud-controller-manager-operator-5f64d86dc5-2fqnb       20m (0%)      0 (0%)      75Mi (0%)        0 (0%)         6h22m
  openshift-cluster-node-tuning-operator       tuned-nv8nz                                                      10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h15m
  openshift-cluster-storage-operator           csi-snapshot-controller-757544fbf6-4s9rx                         10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h18m
  openshift-cluster-storage-operator           csi-snapshot-webhook-68d6b9b485-5m4tj                            10m (0%)      0 (0%)      20Mi (0%)        0 (0%)         6h18m
  openshift-console-operator                   console-operator-5ffb45d94f-mj267                                20m (0%)      0 (0%)      200Mi (1%)       0 (0%)         6h1m
  openshift-console                            downloads-8b57f44bb-k52ft                                        10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h1m
  openshift-controller-manager                 controller-manager-7d4976cb5-k6xcc                               100m (2%)     0 (0%)      100Mi (0%)       0 (0%)         5h59m
  openshift-dns                                dns-default-52gj5                                                60m (1%)      0 (0%)      110Mi (0%)       0 (0%)         6h17m
  openshift-dns                                node-resolver-758kr                                              5m (0%)       0 (0%)      21Mi (0%)        0 (0%)         6h17m
  openshift-etcd                               etcd-guard-master-1.ocp4.tektutor.org.ocp                        10m (0%)      0 (0%)      5Mi (0%)         0 (0%)         6h15m
  openshift-etcd                               etcd-master-1.ocp4.tektutor.org.ocp                              360m (10%)    0 (0%)      910Mi (6%)       0 (0%)         5h54m
  openshift-image-registry                     image-registry-77fc9c6c77-c2dbd                                  100m (2%)     0 (0%)      256Mi (1%)       0 (0%)         5h59m
  openshift-image-registry                     node-ca-xvdg6                                                    10m (0%)      0 (0%)      10Mi (0%)        0 (0%)         5h59m
  openshift-ingress-canary                     ingress-canary-zvtcd                                             10m (0%)      0 (0%)      20Mi (0%)        0 (0%)         6h4m
  openshift-ingress                            router-default-5d8ffdf969-k4t9z                                  100m (2%)     0 (0%)      256Mi (1%)       0 (0%)         6h1m
  openshift-kube-apiserver                     kube-apiserver-guard-master-1.ocp4.tektutor.org.ocp              10m (0%)      0 (0%)      5Mi (0%)         0 (0%)         5h55m
  openshift-kube-apiserver                     kube-apiserver-master-1.ocp4.tektutor.org.ocp                    290m (8%)     0 (0%)      1224Mi (8%)      0 (0%)         5h55m
  openshift-kube-controller-manager            kube-controller-manager-guard-master-1.ocp4.tektutor.org.ocp     10m (0%)      0 (0%)      5Mi (0%)         0 (0%)         6h6m
  openshift-kube-controller-manager            kube-controller-manager-master-1.ocp4.tektutor.org.ocp           80m (2%)      0 (0%)      500Mi (3%)       0 (0%)         5h55m
  openshift-kube-scheduler                     openshift-kube-scheduler-guard-master-1.ocp4.tektutor.org.ocp    10m (0%)      0 (0%)      5Mi (0%)         0 (0%)         6h6m
  openshift-kube-scheduler                     openshift-kube-scheduler-master-1.ocp4.tektutor.org.ocp          25m (0%)      0 (0%)      150Mi (1%)       0 (0%)         6h6m
  openshift-kube-storage-version-migrator      migrator-cfb6c8f7c-lwzmp                                         10m (0%)      0 (0%)      200Mi (1%)       0 (0%)         6h17m
  openshift-machine-config-operator            machine-config-controller-ff46499b5-576g9                        40m (1%)      0 (0%)      100Mi (0%)       0 (0%)         6h16m
  openshift-machine-config-operator            machine-config-daemon-cffz9                                      40m (1%)      0 (0%)      100Mi (0%)       0 (0%)         6h18m
  openshift-machine-config-operator            machine-config-server-wtmwj                                      20m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h16m
  openshift-monitoring                         alertmanager-main-0                                              9m (0%)       0 (0%)      120Mi (0%)       0 (0%)         5h59m
  openshift-monitoring                         node-exporter-lcmqq                                              9m (0%)       0 (0%)      47Mi (0%)        0 (0%)         6h14m
  openshift-monitoring                         prometheus-k8s-0                                                 75m (2%)      0 (0%)      1104Mi (7%)      0 (0%)         5h59m
  openshift-monitoring                         thanos-querier-84dd674795-9wr72                                  15m (0%)      0 (0%)      92Mi (0%)        0 (0%)         5h59m
  openshift-multus                             multus-additional-cni-plugins-2t68k                              10m (0%)      0 (0%)      10Mi (0%)        0 (0%)         6h19m
  openshift-multus                             multus-ctw5b                                                     10m (0%)      0 (0%)      65Mi (0%)        0 (0%)         6h19m
  openshift-multus                             network-metrics-daemon-xnbq2                                     20m (0%)      0 (0%)      120Mi (0%)       0 (0%)         6h19m
  openshift-network-diagnostics                network-check-source-7f6b75fdb6-7vsfs                            10m (0%)      0 (0%)      40Mi (0%)        0 (0%)         6h19m
  openshift-network-diagnostics                network-check-target-95fl2                                       10m (0%)      0 (0%)      15Mi (0%)        0 (0%)         6h19m
  openshift-oauth-apiserver                    apiserver-7c59c579f6-45bdb                                       150m (4%)     0 (0%)      200Mi (1%)       0 (0%)         6h1m
  openshift-operator-lifecycle-manager         packageserver-8589cc98f8-5c6mx                                   10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         6h17m
  openshift-route-controller-manager           route-controller-manager-545b97cd5f-gpbkk                        100m (2%)     0 (0%)      100Mi (0%)       0 (0%)         5h59m
  openshift-sdn                                sdn-controller-nzsqn                                             20m (0%)      0 (0%)      70Mi (0%)        0 (0%)         6h19m
  openshift-sdn                                sdn-wh4kg                                                        110m (3%)     0 (0%)      220Mi (1%)       0 (0%)         6h19m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests      Limits
  --------           --------      ------
  cpu                2048m (58%)   0 (0%)
  memory             7025Mi (48%)  0 (0%)
  ephemeral-storage  0 (0%)        0 (0%)
  hugepages-1Gi      0 (0%)        0 (0%)
  hugepages-2Mi      0 (0%)        0 (0%)
Events:              <none>
</pre>
