---
category: spark
published: true
layout: post
title: Installing Spark 1.4 on CentOS 
description: update the past insatlling method 
---  

## 0. Add User  

```
# switch to root
$ su - 

# add user (dshao is the created username)
$ useradd dshao

# set password 
$ passwd dshao

# put user into sudoers file
$ echo 'dshao ALL=(ALL) ALL' >> /etc/sudoers

``` 



## 1.  Install JDK 1.80 (under root)
 
```
#Find the newest version of JDK ( for me  it is java-1.8.0-openjdk-devel.x86_64)
$ yum search openjdk-devel 

#Install the newest version of JDK 
$ sudo yum install java-1.8.0-openjdk-devel.x86_64

#config java and javac 
$ sudo /usr/sbin/alternatives --config java
$ sudo /usr/sbin/alternatives --config javac

#config  path 
$ sudo vi /etc/profile
       #add the following lines at the end
        export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-devel-1.8.0.45-28.b13.el6_6.x86_64
		export JRE_HOME=$JAVA_HOME/jre
		export PATH=$PATH:$JAVA_HOME/bin
		export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

# save and exit vi

# make the bash profile take effect immediately
$ source /etc/profile

# test
$ java -version
      #result like 
      openjdk version "1.8.0_45"
      OpenJDK Runtime Environment (build 1.8.0_45-b13)
      OpenJDK 64-Bit Server VM (build 25.45-b02, mixed mode)
```  

## 2. Install Scala  (under root)

```
# download file 
 wget http://downloads.typesafe.com/scala/2.11.7/scala-2.11.7.tgz
  
#unzip 
tar xvf scala-2.11.7.tgz

#move into /usr/lib 
sudo mv scala-2.11.7 /usr/lib

#link folders
sudo ln -f -s /usr/lib/scala-2.11.7 /usr/lib/scala

$ sudo vi  /etc/profile.d/scala.sh
       #add the following line at the end
        export PATH=$PATH:/usr/lib/scala/bin

# save and exit vi

# make the bash profile take effect immediately
$ source /etc/profile.d/scala.sh

# test
$ scala -version
    	#result like 
		Scala code runner version 2.11.7 -- Copyright 2002-2013, LAMP/EPFL
```  

　　
## 3. Install Spark with hadoop (under user)

```
# switch to user 
$ su - dshao

# download file 
 wget http://apache.go-parts.com/spark/spark-1.4.0/spark-1.4.0-bin-hadoop2.6.tgz
  
# unzip 
tar xvf spark-1.4.0-bin-hadoop2.6.tgz

# move into spark folder
cd spark-1.4.0-bin-hadoop2.6

# run pyspark
bin/pyspark

``` 

## Scan It!    

![2015-7-10-installing-spark-on-centos.md](../../images/share/2015-7-10-installing-spark-on-centos.md.jpg)