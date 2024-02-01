# Hadoop

## Hadoop Configuration

**core-site.xml**: This file is a part of the Hadoop configuration files, which are used to inform the Hadoop daemon where the NameNode (the centerpiece of an HDFS file system) runs in the cluster³⁴. It contains settings for Hadoop Core, such as I/O settings, that are common to HDFS (Hadoop Distributed File System) and MapReduce³⁴. These settings are crucial for the proper functioning of a Hadoop cluster³⁴.

**NameNode**: In Hadoop, the NameNode is the master node that manages the file system metadata. Each cluster has a single NameNode, and if that machine crashes, the entire Hadoop system goes down³⁴.

**Hadoop Core**: This refers to the basic components of the Hadoop system, including the Hadoop Common (libraries and utilities), HDFS, and MapReduce³⁴.

**HDFS and MapReduce**: HDFS is the primary storage system used by Hadoop applications, while MapReduce is a computational model that allows for processing large data sets in parallel³⁴.

**hdfs-site.xml**: This is a configuration file for Hadoop, specifically for the Hadoop Distributed File System (HDFS) daemons¹³. Daemons are background services running on a system.

**NameNode, Secondary NameNode, and DataNodes**: These are the main components of HDFS¹³. The NameNode is the master server that manages the file system namespace and regulates access to files by clients. The Secondary NameNode works with the NameNode to help ensure the reliability of the data. DataNodes are the workhorses of HDFS, storing and retrieving data blocks when they are told to (by clients or the NameNode), and reporting back to the NameNode periodically with lists of blocks that they are storing¹³.

**Default block replication and permission checking on HDFS**: These are some of the parameters that can be configured in the hdfs-site.xml file¹³. Block replication refers to the number of copies of data blocks. Permission checking refers to the access control on HDFS¹³.

**Replication specified at create time**: When a file is created in HDFS, you can specify the number of replications for that file. If not specified, the default value from the hdfs-site.xml file is used¹³.