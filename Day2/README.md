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
