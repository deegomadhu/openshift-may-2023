# Day 1

## What is Docker?
- container technology
- an application virtualization technology
- this represents a single application not an Operating System

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

