# Day 1

## What is Docker?
- container technology
- an application virtualization technology
- this represents a single application not an Operating System
- based on Linux kernel features
  - namespace
    - is used to isolate an application process from other processes running on the same OS
  - control group (CGroup)
    - is used to apply resource quota restrictions on a container level
    - example
      - we can control how many cpu cores a container can utilize on the system at the max
      - we can control how much RAM a container can utilize on the system where it runs

## What are the Docker alternative tools available
- LXC
- containerd
- CRI-O
- Podman

## What is a Container Engine?
- is a high-level tool that offers user friendly commands to manage images and containers
- example
  - Docker
    - depends on containerd which in turns depends on runC to manage containers
  - Podman

## What is a Container runtime?
- is the low-level tool that actually manages the containers
- these tools are not generally used by end-users like us
- these tools are used by Container Engine
- example
  - CRI-O
  - runC

## What is a Processor?
- is an Integrated Circuit (IC)
- a single processor may support 1 or more CPU Cores
- Server Grade Processors these days support 256/512 Cores per Processor

### What is SCM?
- Single Chip Module
- the IC has just a single Processor

### What is MCM?
- Multiple Chip Module
- you will physically see 1 IC which could internally host/support multiple Processors
- 4/8 Processor per IC

### What is Hyperthreading?
- each physical core doubles up into 2/4/8 virtual cores
- 
## What is a CPU Core?
- represents a single Central Processing Unit
- 
### Total OS required is 1000
- Assume we have a server with Dual Socket with MCM Chip ( 2 Processor per Socket )
- Each Processor supporting 256 Physical Cores each ( Virtual Core 2 x 256 x 2 = 1024 Cores )

## What is Hypervisor?
- generally referred as Virtualization Technology
- Examples
  - VMWare
    - Fusion ( Mac OS-X) - Type 2
    - Workstation ( Linux & Windows ) - Type 2
    - vSphere ( Bare Metal Hypervisor - Type 1 )
  - Oracle
    - VirtualBox - Type 2
  - Parallels ( Mac OS-X)
  - Microsoft
    - Hyper-V
  - Host OS (This is the OS on top of which the Virtualization software is installed)
  - Guest OS (This is the Virtual Machine)
  - Each Virtual Machine represents a fully functional Operating System
    - They get their own dedicated hardwares
    - CPU Cores (Virtual)
    - RAM (Actual size )
    - Storage (HDD/SDD - Actual Size) 
    - Network Card (Virtual)
    - Graphics Card (Virtual)
- Heavy weight virtualization
  - because each Virtual Machine(Guest OS) must be allocated with dedicated hardware resources

## Hypervisor High Level Architecture

## Docker High Level Architecture
- one of the Container technology
- an application virtualization technology
- light-weight
  - they don't need their own dedicated hardwares resources unlike Virtual Machine
- each container represents a single application

## What are similarities between Virtual Machine and a Container ?
- both has their own file systems
- both has IP addresses
- both has dedicated Network Stack

## Docker Image

## Docker Container

## Docker Registries

#### Docker Local Registry

#### Docker Private Registry

#### Docker Remote Registry 

## Network Subnet
Let's take this subnet 172.17.0.0/16
- IPV4 IP address has 32 bits(4 bytes)
- 172(1 byte - 8 bits)
- 17(1 byte - 8 bits)
- 0 (1 byte - 8 bits)
- 0 (1 byte - 8 bits)
- /16 is CIDR
- 172.17.0.0
- 172.17.0.1
- ...
- 172.17.0.255
- 172.17.1.0
- 172.17.1.1 ( Gateway - this is the IP address of docker0 bridge/gateway )
- ...
- 172.17.1.255
- ...
- 172.17.255.255
- Total IP addresses = 256 x 256 = 65536 IP addresses

# Docker Commands

## Finding the docker version
```
docker --version
```

## Finding more details about your docker installation
```
docker info
```

Expected output
<pre>
 jegan@tektutor.org $ <b>docker info</b>
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  compose: Docker Compose (Docker Inc., v2.3.3)

Server:
 Containers: 3
  Running: 0
  Paused: 0
  Stopped: 3
 Images: 30
 Server Version: 20.10.21
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 
 runc version: 
 init version: 
 Security Options:
  apparmor
  seccomp
   Profile: default
  cgroupns
 Kernel Version: 5.19.0-42-generic
 Operating System: Ubuntu 22.04.2 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 48
 Total Memory: 125.5GiB
 Name: tektutor.org
 ID: 7TE4:VNOO:74TD:26WF:VH3Q:FQIN:LIM6:YVQV:RJ63:MY2C:A6ZL:VT33
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
</pre>

## Listing the docker images in your local docker registry
```
docker images
```

## Downloading mysql docker image from Docker Hub Remote Registry to your Local docker registry
```
docker pull mysql:latest
```
Expected output
<pre>
jegan@tektutor.org $ <b>docker pull ubuntu:18.04</b>
18.04: Pulling from library/ubuntu
4e43cebf9258: Pull complete 
Digest: sha256:14f1045816502e16fcbfc0b2a76747e9f5e40bc3899f8cfe20745abaafeaeab3
Status: Downloaded newer image for ubuntu:18.04
docker.io/library/ubuntu:18.04

</pre>

## Finding more details about a docker container image
```
docker image inspect mysql:latest
```

Expected output
<pre>
 jegan@tektutor.org  ~/Desktop  docker image inspect mysql:latest
[
    {
        "Id": "sha256:05db07cd74c0520c8ffe5f7638063719a886f9115cecacc0654d981caf5d27f7",
        "RepoTags": [
            "mysql:latest"
        ],
        "RepoDigests": [
            "mysql@sha256:d6164ff4855b9b3f2c7748c6ec564ccff841f79a7023db0f9293143481a44b6e"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2023-05-24T21:43:13.237785913Z",
        "Container": "f38d8f23cf17014cd5f9a6025dd60d0aac71eb192926e2021c03d06c5d5f5dd3",
        "ContainerConfig": {
            "Hostname": "f38d8f23cf17",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "3306/tcp": {},
                "33060/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.16",
                "MYSQL_MAJOR=8.0",
                "MYSQL_VERSION=8.0.33-1.el8",
                "MYSQL_SHELL_VERSION=8.0.33-1.el8"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"mysqld\"]"
            ],
            "Image": "sha256:a0749de12fb736aa86a85bfda7bdf618dcbf91ce2437875333191090aaba828b",
            "Volumes": {
                "/var/lib/mysql": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "20.10.23",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "3306/tcp": {},
                "33060/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.16",
                "MYSQL_MAJOR=8.0",
                "MYSQL_VERSION=8.0.33-1.el8",
                "MYSQL_SHELL_VERSION=8.0.33-1.el8"
            ],
            "Cmd": [
                "mysqld"
            ],
            "Image": "sha256:a0749de12fb736aa86a85bfda7bdf618dcbf91ce2437875333191090aaba828b",
            "Volumes": {
                "/var/lib/mysql": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 564646609,
        "VirtualSize": 564646609,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/9dbadf4fa0e570573651cdd48b25a28e934df9892d6cf42db0a58666a2d8c7bd/diff:/var/lib/docker/overlay2/31a0daa9c4931f1a647751e66334ed113ba7d0669c54967d454bce6c3ef5e14d/diff:/var/lib/docker/overlay2/7d9c373d215a241bd336bf82b32b7601cae96a32625425bd78d4684865f7722e/diff:/var/lib/docker/overlay2/cd7210049b0b8c4b102ee2dfcb868bb7ce08d834f7d716638b9d2f8e35ec0b53/diff:/var/lib/docker/overlay2/00a006c77b4281d6f907b013337371846c42bbe87ac1e0d106234778689440e1/diff:/var/lib/docker/overlay2/a88a2dfde21fdb1799f7d7c1017f830d350bf53808e97f813a1e11fbaeaf69a5/diff:/var/lib/docker/overlay2/e7cd57269aaa4cda9261717da9bcb1c6d5a4cf0b55610e7567aee973e86d5b10/diff:/var/lib/docker/overlay2/25da735d3ead5b9cfd5db0b06eadd4fa3cdb2cd0bc8e8021c6d7ac4e018f44a4/diff:/var/lib/docker/overlay2/f4d704c58a8ba4a9c222e6637157f5b5c4518345e774ec87fb87cc7eb1a96a58/diff:/var/lib/docker/overlay2/6ac96d49d293ffa1b028773c14777189feff3099b95f86dcc40eff7f61a9af03/diff",
                "MergedDir": "/var/lib/docker/overlay2/a43c2c06d59ef7d75ff51c7437e3802601924210db64cc0411c6df49362df433/merged",
                "UpperDir": "/var/lib/docker/overlay2/a43c2c06d59ef7d75ff51c7437e3802601924210db64cc0411c6df49362df433/diff",
                "WorkDir": "/var/lib/docker/overlay2/a43c2c06d59ef7d75ff51c7437e3802601924210db64cc0411c6df49362df433/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:f9a1099727ada7adafb59d00f8a586db4018c04bb4dc0c8561ec574c0860fb93",
                "sha256:698db29e13b1981197cb0ce710cc5ec8ab882ef375df04710b11c842ccb1b02e",
                "sha256:cd53b79fc46f820449da211a9a2b3b86d39e79d0856de185a40ddc80307d6793",
                "sha256:1f9db33bba3e4cacd66d3ee4b0955e1aa5acdb4bdf7aaf115490b9fa0b0761fa",
                "sha256:bbdc0c28b2fd28e65958c0bed61af66152c193dd27077287424e5282a8677f44",
                "sha256:ab366f7baef0c2362d90fab3ee49b4d298e192a5d6b54065b4145cb1001d5621",
                "sha256:e19c4f39b626a33c89f93bac4c0bc9a820041bb4f7cfc88cf573e3cc57864a18",
                "sha256:eba93af91d818c69e82c3d5f46e09f2952a32d43fa5c236d40c9d8418f1c74af",
                "sha256:baaa5d2f07a7e78f4999c5f5f59aa3b6973948895cb1a9e9c621d1b7680f1d7a",
                "sha256:ecc3fd0b4a47f15a38ccee317f6dfbe21006ed5a65ee86395afbc83876b52336",
                "sha256:409c7593682e8197611f748dd744b022ddb4054c79b7b8709a6f9557fe6c94c5"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
</pre>

## Deleting a Docker image
```
docker rmi ubuntu:20.04
```

Expected output
<pre>
jegan@tektutor.org $ <b>docker rmi ubuntu:20.04</b>
Untagged: ubuntu:20.04
Untagged: ubuntu@sha256:db8bf6f4fb351aa7a26e27ba2686cf35a6a409f65603e59d4c203e58387dc6b3
Deleted: sha256:88bd6891718934e63638d9ca0ecee018e69b638270fe04990a310e5c78ab4a92
Deleted: sha256:6f37ca73c74f2cef0ddefd960260f2033c16c84583c5507a4f37b1cf7631dc20
</pre>

## Creating a container in the background mode
```
docker run -dit --name c1 --hostname c1 ubuntu:22.04 /bin/bash
```

Expected output
<pre>
jegan@tektutor.org $ <b>docker run -dit --name c1 --hostname c1 ubuntu:22.04 /bin/bash</b>
4e26ffa1ed02eda5090f3388bbda599e13368f6ed38249d2c11bf412651429a4
</pre>

List the running containers
<pre>
jegan@tektutor.org $ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS     NAMES
4e26ffa1ed02   ubuntu:22.04   "/bin/bash"   3 seconds ago   Up 2 seconds             c1
</pre>

## Problems that a loadbalancer solves ( usecases for load balancers )
1. To handle the application traffic quickly with many servers/applications
2. To ensure high-availability
3. To improve security


## ⛹️‍♂️ Lab - Setup a Load Balancer with nginx

Let's create 3 web servers with nginx docker image
```
docker run -d --name nginx1 --hostname nginx1 nginx:latest
docker run -d --name nginx2 --hostname nginx2 nginx:latest
docker run -d --name nginx3 --hostname nginx3 nginx:latest
```

Let's list the containers and check if all the nginx web servers are running
```
docker ps
```

Let's create the load balancer container
```
docker run -d --name lb --hostname lb nginx:latest
```

Let's list the containers and check if all the nginx web servers and lb container are running
```
docker ps
```

Now we need to configure the lb container to work like a load balancer, hence let's copy the nginx.conf file from container to local machine to configure it
```
docker cp lb:/etc/nginx/nginx.conf .
```

Edit the nginx.conf on your local machine with the below content
```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}

http {
    upstream backend {
        server 172.17.0.2:80;
        server 172.17.0.3:80;
        server 172.17.0.4:80;
    }
    
    server {
        location / {
            proxy_pass http://backend;
        }
    }
}
```

In the above file, 172.17.0.2 is my nginx1 IP address, 172.17.0.3 is the nginx2 IP address and 172.17.0.4 is the nginx3 container's IP Address. Update them after checking your nginx container IP addresses accordingly.

Now let's copy the nginx.conf from local machine to the lb container
```
docker cp nginx.conf lb:/etc/nginx/nginx.conf
```

To apply the config change, we need to restart the container
```
docker restart lb
docker ps
```

We can also update the index.html files on nginx1, nginx2 and nginx3 to verify the pages are really coming from nginx1, nginx2 and nginx3 web servers.
```
echo "Web Server 1" > index.html
docker cp index.html nginx1:/usr/share/nginx/html/index.html

echo "Web Server 2" > index.html
docker cp index.html nginx2:/usr/share/nginx/html/index.html

echo "Web Server 3" > index.html
docker cp index.html nginx3:/usr/share/nginx/html/index.html
```

Now, its time to verify if the Load Balancer is working as configured. Let's find the IP address of our lb container
```
docker inspect -f {{.NetworkSettings.IPAddress}} lb
```

In my case, the lb container's IP address happens to be 172.17.0.5, hence on my lab browser
I can access the 172.17.0.5 to see the traffic getting routed to different nginx containers in a round robin fashion.

## ⛹️‍♂️ Lab - Accessing your applications running within containers from external machine using Port Forwading

Assuming your nginx1, nginx2 nginx3 and lb containers are already running. Let's delete only the lb container to perform port-forwarding on our new lb container.

```
docker rm -f lb
docker run -d --name lb --hostname lb -p 8001:80 nginx:latest
```
In the above run command, you may have to replace 8001 with some other available port in case someone has already used it on your CentOS server.

We need to copy the nginx.conf load balancer configuration that we did in our previous lab into the new lb container.
```
docker cp nginx.conf lb:/etc/nginx/nginx.conf
```

Let's restart the lb container to apply config changes.
```
docker restart lb
docker ps
```

Now you should be access the lb setup from your RPS Windows lab machine web browser
```
10.10.15.2:8001
```

## Lab - Using external storage to save your application data
```
ls -l /tmp/mysql*
mkdir -p /tmp/mysql
docker run -d --name mysql --hostname mysql -e MYSQL_ROOT_PASSWORD=root@123 -v /tmp/mysql:/var/lib/mysql mysql:latest
docker ps
```

Now let's get inside the mysql container shell
```
docker exec -it mysql sh
```

Let's connect to the mysql server
```
mysql -u root -p
```
When it prompts for password, type 'root@123' without the quotes.

Let's create a database
```
CREATE DATABASE tektutor;
USE tektutor;
CREATE TABLE training ( id INT NOT NULL, name VARCHAR(100), duration VARCHAR(100), PRIMARY KEY(id) );
```

Let's insert some records into the training table
```
INSERT INTO training VALUES ( 1, "Docker and Kubernetes", "5 Days" );
INSERT INTO training VALUES ( 2, "Microservices with Go lang", "5 Days" );
INSERT INTO training VALUES ( 3, "OpenShift", "5 Days" );
```

Let's list the records
```
SELECT * FROM training;
```

Let's exit from the mysql prompt and mysql container
```
exit
exit
```

Let's delete the mysql container
```
docker rm -f mysql
docker ps
```

Let's recreate a new mysql and mount the same external volume location
```
docker run -d --name mysql --hostname mysql -e MYSQL_ROOT_PASSWORD=root@123 -v /tmp/mysql:/var/lib/mysql mysql:latest
docker ps
```

Let's get inside the container
```
docker exec -it mysql sh
mysql -u root -p
```
When it prompts for password, type root@123

Try the below
```
SHOW DATABASES;
USE tektutor;
SHOW TABLES;
SELECT * FROM training;
```

You are supposed to see the records in tact as we used stored the mysql records in an external volume storage.
