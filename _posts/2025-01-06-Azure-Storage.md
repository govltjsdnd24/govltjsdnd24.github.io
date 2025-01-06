---
categories: [ Study, Azure Storage ]
tags: [ cloud ] 
---


## Storage Types and Endpoints

Microsoft Azure provides cloud storage access via means of unique namespaces called storage accounts. These storage accounts are classified into different types according to their redundancy options:
- LRS (Locally Redundant Storage)
- GRS (Geo Redundant Storage)
- RA-GRS (Read-Access Geo Redundant Storage)
- ZRS (Zone Redundant Storage)
- GZRS (Geo-Zone Redundant Storage)
- RA-GZRS (Read-Access Geo-Zone Redundant Storage)

Storage account endpoints are formed by combining the account name with azure storage service endpoint. The Azure Storage service endpoints follow such formats:
- Blob : https://<storage-account-name>.blob.core.windows.net
- Data Lake Storage Gen2 : https://<storage-account-name>.dfs.core.windows.net
- Azure File : https://<storage-account-name>.file.core.windows.net
- Queue Storage : https://<storage-account-name>.queue.core.windows.net
- Table Storage : https://<storage-account-name>.table.core.windows.net

## Storage Redundancy

Azure Storages always create copies of data in order to protect it from unforseen errors. This means that redundancy equates to the data's level of sturdiness.  

Azure storage account's data is always replicated three times in the default area. LRS and ZRS are offered as options for data replication in the primary region.

Locally Redundant Storages copy data thrice within the primary region. It provides 99.999999999% durability for the designated 1 year. Being the cheapest option, LRS has the lowest durability amongst the storage options. It can provide protection from server rack and drive errors, but is susceptible to physical disasters.

Zone Redundant Storages synchronously copies data across three availability zones within Azure. It provides over 99.9999999999% of durability. ZRS enables data read and write even when an availability zone is unusable, because Azure runs a DNS relocation network update to distribute traffic to another zone. This allows a high level of availability.

## Secondary Region Redundancy

When an application requires a high level of durability, it may choose to replicate data to a secondary region located far away from the primary one. Azure Storage provides two optons for copying data to a secondary region: GRS and GZRS. GRS is similar to running a LRS in two regions, and GZRS to running a ZRS in the primary region and LRS in the second one.

Data is typically replicated between the primary and secondary regions asynchronously, so when a sudden disaster happens, there can be a RPO that resides in the most recent writes between the primary and secondary regions. Most of the time, the RPO is under 15 minutes.

Geo Redundancy Storages run LRS in two distinct regions,while Geo Zone Redundancy Storage runs ZRS in the primary region and LRS in the secondary one. GZRS is mostly used in applications that require maximum uniformity, durability, availability, high performance and restorability. 

Reads in the secondary zone becomes available only when failover happens after the primary zone becomes unusuable. Of course, we could make the secondary zone accessible at all times through RA-GRS and and RA-GZRS. (The secondary zone may not be completely new due to RPO).


## Azure Storage Services

There are multiple data services provided at the Azure Storage platform: 
- Azure Blob : Object storage excellent at expandabilit for text and binary data (Provides big data analysis through Data Lake Storage Gen2)
- Azure Files : File storage for cloud or on-premise distribution
- Azure Queue : Messaging storage for a stable messaging between application components
- Azure Disk : Block-level storage volume for Azure VM
- Azure Table : No-SQL table option for structured non-relational data

Azure Blob Storage enables storage of unstructured--unlimited data type--vast amount of data, allowing infinitely expanding pool of log files. A single advantage of blob storage of disk storage is that the developer doesn't have to manage the disk; Azure will process the requirements for the physical sotrage. Blobs are advised when : 
- Browsers directly provide images or documents
- Files are saved for distributed access
- Video or audio are used for streaming
- Data is dedicated for backup/restoration, disasiter recovery or saving
- Data is saved for analysis at on-premise or Azure hosting service


## Blob Storage

Blob storages can be accessed anywhere through HTTP or HTTPS access. Since data within the cloud can multiply exponentially, data can be allocated to layers depending on their properties such as data access frequency or storage period.
- Hot Access Level
- Cool Access Level
- Cold Access Level
- Archive Access Level

## Other Storages

Azure File Storage provides file shares accessible through protocols such as SMB or NFS. SMB Azure file shares can be cached in Windows Server for faster access at the region near the data access.

Azyre Queues provide messaging service through HTTP or HTTPS. Each message has a maximum size of 64KB and is generally used for creating backlogs of tasks to be completed asynchronously.

Azure Disk Storages are block-level storage volumes that is logically indentical to an actual disk, but is vritualized for increased availability and resiliency.

Azure Tables can used to build a hybrid or multiple cloud solution whiere data is readily availabe, and overall suitable for creating a structured non-relational database.

## Azure Data Migration Options

Azure Migrate is a service that helps migration from on-premise environment to the cloud, serving as a hub between the two. These functions are provided: 
- Unified migration platform
- Range of tools (For assessment and migration)
- Assessment and migration

Azure Migrate hub contains integrated tools such as:
- Azure Migrate
- Data Migration Assistant
- Azure Database
- Azure App Service Migration Assistant
- Azure Data Box

Azure Data Box is a physical migration service provides a cheap yet fast and reliable transmission of large amounts of data. The max storage capacity is 80 TeraBytes which is protected within a rugged case during transportation. Examples of Data Box usage for dispatch to Azure is:
- One-time Migration
- VM Farm
- Initial Large Transmission
- Frequent Upload
- Transition from Offline Tape to Azure Media Library

Examples of Data Box usage for dispath from Azure is: 
- Disaster Recovery
- Security Requirement
- Migration to On-premise or another Cloud Service Provider

## Azure File Transfer Options

Azure offers smaller data transfer options, too. AzCopy is a command-line utility that can be used for copying blobs or files to and from storage accounts. It can be set so that data can be interchanged with other cloud service probiders. Do keep in mind that blos or files transfers are unilateral, and doesn't automatically synchronize data between two environments.

Azure Storage Explorer offers a GUI for Azure file transfer, Azyre File Synchronize offers a contstruction of a certralized file sharing while maintaining the flexibility, performance, and compatibility or Window Servers.


## Reference

[https://learn.microsoft.com/ko-kr/training/modules/describe-azure-storage-services/](https://learn.microsoft.com/ko-kr/training/modules/describe-azure-storage-services/)

