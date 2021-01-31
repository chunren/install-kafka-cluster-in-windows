# How To Set Up Apache Kafka Cluster on Window 10

### [By Chunren Lai](https://github.com/chunren), Jan.30, 2021

This article lists steps to install and run Apache Kafka cluster on Windows 10.

## Table of Contents  
[Step 1. Introduction](#Step-1-Introduction)  
[Step 2. Download Files](#Step-2-Download-Files)  
[Step 3. Install the 7zip and Notepad++](#Step-3-Install-the-7zip-and-Notepad-plus-plus)  
[Step 4. Install the Java Runtime](#Step-4-Install-the-Java-Runtime)  
[Step 5. Install ZooKeeper](#Step-5-Install-ZooKeeper)  
[Step 6. Install and Set up Kafka Cluster](#Step-6-Install-and-Set-up-Kafka-cluster)  
[Step 7. Test Apache Kafka Cluster](#Step-7-Test-Apache-Kafka-cluster)  

## Step 1. Introduction
To run Apache Kafka cluster on a windows OS, you can refer my article - [How To Set Up Apache Kafka on Window 10](https://github.com/chunren/install-kafka-on-windows), prepare and install all for the first five steps. 

## Step 2. Download Files
Ref - [Download Files](https://github.com/chunren/install-kafka-on-windows#Step-2-Download-Files)

## Step 3. Install the 7zip and Notepad plus plus
Ref - [Install the 7zip and Notepad++](https://github.com/chunren/install-kafka-on-windows#Step-3-Install-the-7zip-and-Notepad-plus-plus)

## Step 4. Install the Java Runtime
Ref - [Install the Java Runtime](https://github.com/chunren/install-kafka-on-windows#Step-4-Install-the-Java-Runtime)

## Step 5. Install ZooKeeper
Ref - [Install ZooKeeper](https://github.com/chunren/install-kafka-on-windows#Step-5-Install-ZooKeeper)

## Step 6. Install and Set up Kafka Cluster
Once you have finished the install the Zookeeper,
- step 6.1. Use 7zip to unzip the Kafka's installation file (e.g., "kafka_2.13-2.7.0.tgz"). You will need to unzip it twice to get the original files.
- step 6.2. After you fully unzip it, you will have a folder like:
C:\temp\KafkaDownloads\kafka_2.13-2.6.0\kafka_2.13-2.6.0\kafka_2.13-2.6.0
![Kafka unzip](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_unzip_chunren_lai_2020.png)
- step 6.3. Move the unzipped folder to C:\, and rename it as: C:\kafka_1, and you will see:
    ![kafka_1](https://github.com/chunren/markdown-src/blob/master/raw/images/kafka_1_chunren_lai.jpg)
- step 6.4. Make a new subfolder C:\kafka_1\kafka-logs
- step 6.5. Edit the  C:\kafka_1\config\server.properties, modify the following line with the new value:
```sh
broker.id=1
```
```sh
listeners=PLAINTEXT://localhost:9091
```
```sh
log.dirs=c:/kafka_1/kafka-logs
```
see the screenshot below: 
![kafka_1 server settings](https://github.com/chunren/markdown-src/blob/master/raw/images/kafka_1_server_setting_chunren_lai.png)

- step 6.6. Copy the folder C:\kafka_1, and change the new folder as: C:\kafka_2
- step 6.7. Edit the  C:\kafka_2\config\server.properties, modify the following line with the new value:
```sh
broker.id=2
```
```sh
listeners=PLAINTEXT://localhost:9092
```
```sh
log.dirs=c:/kafka_2/kafka-logs
```

- step 6.8. Copy the folder C:\kafka_1, and change the new folder as: C:\kafka_3
- step 6.9. Edit the  C:\kafka_3\config\server.properties, modify the following line with the new value:
```sh
broker.id=3
```
```sh
listeners=PLAINTEXT://localhost:9093
```
```sh
log.dirs=c:/kafka_3/kafka-logs
```


## Step 7. Test Apache Kafka Cluster
- Go to the home directory of each Kafka folder (e.g., C:\kafka_1, C:\kafka_2 and C:\kafka_2), and run the following commands.
1) Open a new command prompt, and type: 
```sh 
cd c:\kafka_1, and press enter
.\bin\windows\kafka-server-start.bat .\config\server.properties
```
2) Open a new command prompt, and type: 
```sh 
cd c:\kafka_2, and press enter
.\bin\windows\kafka-server-start.bat .\config\server.properties
```
3) Open a new command prompt, and type: 
```sh 
cd c:\kafka_3, and press enter
.\bin\windows\kafka-server-start.bat .\config\server.properties
```

- Go to the home directory of any one Kafka folder, for example, to run the following command:
```sh 
cd c:\kafka_1, and press enter
.\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 3 --partitions 6 --topic StudentImport
.\bin\windows\kafka-topics.bat --list --zookeeper localhost:2181 
```
![topic created](https://github.com/chunren/markdown-src/blob/master/raw/images/kafka_cluster_create_topic_chunren_lai.png)

- Check the topic detail in Kafka cluster:
```sh 
cd c:\kafka_1, and press enter
.\bin\windows\kafka-topics.bat --zookeeper localhost:2181 --describe --topic StudentImport
```
![topic details](https://github.com/chunren/markdown-src/blob/master/raw/images/kafka_cluster_topic_chunren_lai.png)

<style>
.alert-green {
  color: rgb(60,118,61) !important;
}
</style>

<span class="alert-green ">**Congratulations!**></span> You have successfully set up \textcolor{<green>{**Apache Kafka Cluster**} on your Windows 10.
