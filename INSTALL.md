# Overview

Insert some overview text.

## Hadoop Install Tasks

1. Build a VM with 2 x vCPUs and 8GB of RAM using VMware Workstation or VirtualBox.
2. Download ISO of Ubuntu 16.04LTS Server and install.
3. Install Ubuntu Desktop:  `sudo apt-get install ubuntu-desktop`
4. Install OpenJDK Java:  `sudo apt-get install default-jdk`
5. Download latest version of Apache Hadoop:  http://apache.cs.utah.edu/hadoop/common/stable/  (Pull down the binary Gz file, not the src Gz).
  * Install SSH and Rsync:  `sudo apt-get install ssh rsync`
6. Expand Hadoop binary gzip:  `tar -zxf hadoop-x.x.x.tar.gz`
7. Edit **etc/hadoop/hadoop-env.sh** and add the following:

  `export JAVA_HOME=/usr/lib/jvm/default-java`
  
8. Test install with the following command:

  `$ bin/hadoop`
  
## HDFS Install Tasks

1. Make the following edits to the HDFS configuration files:

**etc/hadoop/core-site.xml:**

```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

**etc/hadoop/hdfs-site.xml:**

```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

2. Generate keys for SSH Passphraseless login:
NOTE: Be careful that you use RSA encryption when using a newer version of Ubuntu.  As of OpenSSH 7.0, DSA encyrption as been deprecated.  Older Hadoop documentation still references DSA key creation.

```
$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
````

3. Test Passphraseless login: `ssh localhost`
NOTE: If this does not work, check the /var/log/auth.log for errors.



