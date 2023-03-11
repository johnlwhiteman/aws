# 06: EC2 Instance Storage

## EBS Overview

* Elastic Block Store (EBS) volume is a network drive you can attach to your instances while they run
* It allows your instances to perist data, ever after their termination
* They can only be mounted to one EC2 instances at a time
  * You can mount multiple EBSs to one EC2 though
  * EBS can be unattached to ... later to be used
* They are bound to a specific availability zone
* Analogy: Think of them as a "network USB stick"
* Free tier: 30GB of free EBS storage of type General Purpose (SSD) or Magnetic per month
* Network drive, not a physicaldrive
  * Network can mean latency, more so than say if using a physical drive
  * It can be detached from an EC2 instance and attached to another one quickly
* Locked to an availability zone (AZ)
  * EBS Volume in one AZ and be attached to another in a different AZ
* Have a provisioned capacity (size in BGs and IOPS)
  * You get billed for all the provisioned capacity
  * You can increase capacity of the drive over time
* EBS has a delete on terminatoin attribute
  * By default is ticked for the root volume 
    * This means that the EBS is deleted when EC2 terminates
  * Any other non-root volume is not deleted by default when EC2 terminates

## EBS Multi-Attach

* io1 and io2 volume types do allow multiple instances to attach to them
  * This probably won't be on exam but just in case

## EBS Snapshots Overview

* Make a backup (snapshot) of you EBS volume at a point in time
* Not necessary to detach volume to do snapshot, but recommended
* Can copy snapshots scross AZ or region
* Can use snapshot in to restore to another AZ
* EBS Snapshot Archive
  * Move a snapshot to an "archive tier" that is 75% cheaper
  * Takes within 24 to 72 hours for restoring the archive
* Recycle Bin for EBS Snapshots
  * Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
  * Specify retention from 1 day to 1 year

## AMI Overview

* AMI - Amazon Machine Image
* AMI are a customization of an EC2 instance
  * Add your own software, configuration, operating system, monitoring ...
  * Faster boot / configuration time because all your software is pre-packaged
* AMIs are built for a specific region (and can be copied across regions)
* You can launch EC2 instnaces from:
  * A public AMI: AWS provided
  * Your own AMI: you make and maitain them yourself
  * An AWS markeplace AMI: an AMI someone else made (and potentially sells)

## AMI Process from an EC2 Instance

* Start an EC2 instance and customize it
* Stop the instance (for data integrity)
* Build an AMI - this will also create EBS snapshots
* Launch instances from other AMIs

## EC2 Image Builder Overview

* New service
* Used to automate the creation of Virtual Machines or container images
  * Automate the create, maintain, validate, and test EC2 AMIs
* Can be run on a schedule (weekly, whenever packages are updated, etc...)

```
[EC2 Image Builder] -> create -> [Build EC2 Instance] -> create -> [New AMI] -> Test EC2 Instance -> AMI is distributed to mutliple regions
```

## EC2 Instance Store (hw disk attached)(ephermeral)

* EBS volumes are network drives with good but "limited" performance
* If you need "high" performance hw disk, used EC2 Instance Store
* Better I/O performance
* EC2 Instance Store lose their storage if they're stopped (ephemeral)
* Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails
* Backups and replication are your responsibility

## EFS Overview (NFS)

* Managed NFS (network file system) that can be mounted on 100s of EC2 instances
* EFS works with Linux EC2 instances in multi-AZ only
* Highly available, scalable, expensive (3x gp2) pay per use, no capcity planning

### EBS vs EFS

* EBS volume can only attach to one instance in same AZ
* EFS in network volume, many instances from multiple AZs can connect to EFS

### EFS Infrequent Access (EFS-IA)

* Storage class that is cost-optimized for files not access every day
* Up to 92% lower cost compared to EFS Standard
* EFS will automatically move your files to EFS-IA based on the last time they were accessed
* Enable EFS-IA with a Lifecycle Policy
  * Example: move file that are not accessed for 60 days to EFS-IA
* Transparent to the applications accessing EFS

## Shared Responsibility Model for EC2 Storage

### AWS

* Infrastructure
* Replication for data for EBS volumes & EFS drives
* Replacing faulty hardware
* Ensuring their employees cannot access your data

### You

* Setting up backup / snapshot procedures
* Setting up data encryption
* Responsibility of any data on the drives
* Understanding the risk of using EC2 Instance Store

## Amazon FSx Overview (3rd Party)

* Launch 2rd party high-performance file systems on AWS
* Fully managed service
* Three Offerings
  1. FSx for Lustre
  2. FSx for Windows File Server
  3. FSx for NetApp ONTAP

### FSx for Lustre (Linux + Cluster)

* Fully managed, high-performance, scalable file storage for High Performance Computing
* The name Lustre is derived from "Linux" and "cluster"
* Machine Learning, Analytics, Video Processing, Financial Modeling, ...
* Scales to 100s GB/s, millions of IOPS, sub-ms latencies

## EC2 Instance Storage Summary

* EBS volumes
  * Network drives attached to one EC2 instance at a time
  * Mapped to an Availability Zone
  * Can use EBS Snapshots for backups / transferring EBS volumes across AZ
* AMI: Create ready-to-use EC2 instances with our customizations
* EC2 Image Builder: Automatically build, test, and distribute AMIs
* EC2 Instance Store:
  * High performance hardware disk attached to our EC2 instance
  * Lost if our instance is stopped /terminated
* EFS: Network file system, can be attached to hundreds of instances in a region
* EFS-IA: Cost-optimized storage class for infrequent accessed files
* FSx for Windows: Network File System for Windows servers
* FSx for Lustre: High performance Computing Linux file system

## Quiz

* An EBS Volume is a network drive you can attach to your instances while they run, so your instances' data persist even after their termination.

* EBS Volumes are tied to only one availability zone.




### FSx for Windows File Server

* Fully managed, highly reliable, and scalable Windows native shared file system
* Built on Windows File Server
* Supports SMB protocol and Windows NTFS
* Integrated with Microsoft Active Directory
* Can be accessed from AWS or your on-premise infrastructure



## References

