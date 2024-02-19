# Setup Redis Instances Manually

|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Khushi Malhotra |  13 Feb 2024  |  Version 1 | Khushi Malhotra  | 13 Feb 2024    |
***
# Table of Contents
- [Introduction](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#introduction)
- [Pre-requisites](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#pre-requisites)
- [Setup Redis Manually](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#setup-redis-manually)
- [Conclusion](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#conclusion)
- [Contact Information](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#contact-information)
- [Resources and References](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Instances/README.md#resources-and-references)
***

# Introduction
Redis can be used as a database, cache, streaming engine, message broker, and more.
Redis Cluster provides a way to run a Redis installation where data is automatically sharded across multiple Redis nodes. Redis Cluster also provides some degree of availability during partitions—in practical terms, the ability to continue operations when some nodes fail or are unable to communicate.
So, with Redis Cluster, you get the ability to:
- Automatically split your dataset among multiple nodes.
- Continue operations when a subset of the nodes are experiencing failures or are unable to communicate with the rest of the cluster.

# Pre-requisites
| Tool         |  Instance Type  |
|--------------|-----------------|
| AWS Instance | t2.medium       |

| Tool         | Command |
|--------------|---------|
| netstat      | `sudo apt install net-tools`|

| Security Protocol | 
|-------------------|
| [Security Group](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Security_Group/README.md)   | 

# Setup Redis Manually
***
## Installing Redis
**Step-1** Launch 3 EC2 Instances
- Sign in to the AWS Management Console.
- Go to the EC2 dashboard.
- Launch a new EC2 instance using an Ubuntu Server AMI (Amazon Machine Image).
- Instance type - t2.medium

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/a31570b3-d169-4d0a-9252-6ce9ea934848)


**Step-2** [Security Group Configuration](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Security_Group/README.md)
- Create 3 security group.

**Step-3** Connect to your EC2 Instances
- Once the instance is running, connect to it using SSH. The private key associated with the key pair selected at launch will be required.

**Step-4** Install Redis on Each Server
- Update the package index
```Shell
  sudo apt update
```
- Install Redis server
```shell
sudo apt install redis-server
```
- To check whether Redis is running on your server, you can use the following command
```Shell
sudo systemctl status redis-server
```

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/37220e92-31c2-4841-b6de-be9fe6d98fb8)

- Configure Redis Instances
  1. Edit the Redis configuration file in each server:
```shell
sudo nano /etc/redis/redis.conf
```

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/b1c65664-abea-41d0-972c-667c879272b5)

  2. Find the line `bind 127.0.0.1` and replace it with `bind <server1_IP>`. Replace `<server1_IP>` with the private IP address of the servers.

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/293c39d3-05bc-4b20-b59e-93b17104b75f)

  3. Find the line `protected-mode yes` and change it to `protected-mode no` to allow external connections.
  4. Fnd the line `port 6379` and uncomment it.

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/c4a22e99-c917-4ad0-88c3-ea9f6eb7c2a7)

  5. Find the line `cluster-enabled no` and change it to `cluster-enabled yes`.
  6. Find the line `cluster-config-file nodes-6379.conf` and uncomment it.
  7. Find the line `cluster-node-timeout 150000` and uncomment it.

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/e16543c0-e452-4af3-86cd-9548d747b3df)


  5. Save and close the file.

**Step-5** Restart Redis Service
- Restart the Redis service on each server to apply the configuration changes
```shell
sudo systemctl restart redis-server
```
```Shell
sudo systemctl status redis-server
```

**Step-6** Verify Configuration
- Check that Redis is running and listening on the correct IP addresses and ports.
```Shell
sudo netstat -tuln | grep 6379
```
![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/88c94403-defa-46da-bfee-4a55ba3d06a6)

**Step-7** To check the logs of each Redis node for error messages or warnings, you'll typically need to access the log files generated by Redis.
- Using tail: If you want to monitor the log file in real-time for new entries, you can use the tail command with the -f option.
```shell
tail -f /var/log/redis/redis-server.log
```
If this Warning message is displayed on your screen.

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/3e9d0bce-d2d7-478e-ab6d-da0ab068e9fc)

This warning suggests that the overcommit_memory setting is not optimized for Redis, which may cause issues with background saves under low memory conditions. It's recommended to follow the instructions provided in the warning message to adjust the overcommit_memory setting.
you can run the command directly without persisting it
```shell
sysctl vm.overcommit_memory=1
```
After making this change, it's advisable to restart the Redis service for the new configuration to take effect. You can do this using the following command
```shell
sudo systemctl restart redis-server
```

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/d51cb988-c1ca-4178-be24-67b03b5bc323)

**Step-8** Create the Redis Cluster:
- On Server 1, run the following command to create the Redis cluster
```shell
redis-cli --cluster create <server1_IP>:6379 <server2_IP>:6379 <server3_IP>:6379 --cluster-replicas 0
```

**Step-9** Check Cluster info 
- To check the status and information of your Redis cluster, you can use the redis-cli tool with the cluster command.
```shell
redis-cli -h <node_IP_address> -p <port_number>
```
```shell
cluster info
```
```shell
cluster nodes
```

![image](https://github.com/CodeOps-Hub/Documentation/assets/156056460/8584dd07-6068-4944-a3ac-f9cfd4bb2448)

### Cluster has been created successfully

# Conclusion
Redis installation and Redis cluster manually in a well-planned and secure manner, ensuring reliability, performance, and scalability for your applications.

# Contact Information
| Name            | Email Address                        |
|-----------------|--------------------------------------|
| Khushi Malhotra | khushi.malhotra.snaatak@mygurukulam.co |

# Resources and References 
| Reference | Link |
|-----------|------|
| Security Group | [Ports Defining](https://github.com/CodeOps-Hub/Documentation/blob/main/Infra/Manual/Redis_Setup/Security_Group/README.md)
| Redis cluster | [Redis official document](https://redis.io/docs/management/scaling/) |
| Configuring the clusters | [stackoverflow](https://stackoverflow.com/questions/39568561/how-to-solve-redis-cluster-waiting-for-the-cluster-to-join-issue)|
| Redis Specification | [Specification redis doc](https://redis.io/docs/reference/cluster-spec/)|








