# HadoopLearning
Learning materials for Hadoop eco system


## Hadoop pre condition commands

### Update and Java instalation
`$ sudo apt update`<br>
then<br>
`$ sudo apt install openjdk-8-jre-headless`<br>

### Add new user and user groop for Hadoop
`$ sudo addgroup hadoop`<br>
then<br>
`$ sudo adduser --ingroup hadoop hadoopusr`<br>
follow the instructions and creat the user.

### Add the new hadoopusr to the sudo users group
`$ sudo adduser hadoopusr sudo`<br>

### Install the openssh server
`$ sudo apt install openssh-server`<br>

### Switch to hadoopusr
Use below comand to switch to hadoopusr and use the hadoopusr's password when promped.<br>
`$ su hadoopusr`<br>

### Generate ssh key and add it to authorized keys
This command will generate a ssh key<br>
`$ ssh-keygen -t rsa -P ""`<br>
This command will add the generated public key to the authorized keys of the host machine<br>
`$ cat $HOME/ .ssh/id_rsa.pub >> $HOME/ .ssh/authorized_keys`<br>

### Verify the ssh configuration
`$ ssh localhost`
you will be ssh into the localhost (in this case the same machine). <br>
use below comad to exit<br>
`$ exit`

## Hadoop installations commands

### Download and extract hadoop
Download the prefered hadoop distribution from apache hadoop repository <br>
https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz

extrat the file using <br>
`$ sudo tar -xvzf hadoop-2.9.2.tar.gz`

Move the extracted files to hadoop user folder<br>
`$ sudo mv hadoop-2.9.2 /usr/local/hadoop`

Change the ownership of the moved folder to hadoopusr<br>
`sudo chown -R hadoopusr /usr/local/hadoop`

### Update the .bashrc with environment variables
`$ sudo gedit ~/.bashrc`<br>

Append below to the file
~~~~
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
~~~~

then reload the updated .bashrc with<br>
`$ source ~/.bashrc`

### Update the hadoop-env.sh
`$ sudo gedit /usr/local/hadoop/etc/hadoop/hadoop-env.sh`

Replace the JAVA_HOME with this<br>
`export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64`

### Update the core-site.xml
`$ sudo gedit /usr/local/hadoop/etc/hadoop/core-site.xml`

Add the below property to the configuration<br>
~~~~
<property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:9000</value>
</property>
~~~~

### Update the hdfs-site.xml
`$ sudo gedit /usr/local/hadoop/etc/hadoop/hdfs-site.xm`

Add the below properties to the configuration
~~~~
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>
<property>
  <name>dfs.namenode.name.dir</name>
  <value>file:/usr/local/hadoop_tmp/hdfs/namenode</value>
</property>
<property>
  <name>dfs.datanode.data.dir</name>
  <value>file:/usr/local/hadoop_tmp/hdfs/datanode</value>
</property>
~~~~
### Update the yarn-site.xml
`$ sudo gedit /usr/local/hadoop/etc/hadoop/yarn-site.xml`

Add the below properties to the configuration<br>
~~~~
<property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
<property>
  <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
~~~~

### Copy and rename the mapred-site.xml.template to mapred-site.xml and update
`$ sudo cp /usr/local/hadoop/etc/hadoop/mapred-site.xml.template /usr/local/hadoop/etc/hadoop/mapred-site.xml`<br>

`$ sudo gedit  /usr/local/hadoop/etc/hadoop/mapred-site.xml`<br>

Add the below properties to the configuration<br>
~~~~
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>
~~~~

### Make HDFS directories same as given in the config
`$ sudo mkdir -p /usr/local/hadoop_tmp`
`$ sudo mkdir -p /usr/local/hadoop_tmp/hdfs`
`$ sudo mkdir -p /usr/local/hadoop_tmp/hdfs/namenode`
`$ sudo mkdir -p /usr/local/hadoop_tmp/hdfs/datanode`

### Make the hadoopusr the owner of the hdfs folder
`$ sudo chown -R hadoopusr /usr/local/hadoop_tmp`


## Starting up the Hadoop 

### Format the hdfs namenode
`hdfs namenode -format`

### Start the hdfs
`start-dfs.sh`

### Start the yarn
`start-yarn.sh`

### Verify the running 
`jps`

if you get the response like below then hadoop is installed correctly
~~~~
hadoopusr@hadoopvm:~$ jps
8801 DataNode
9474 NodeManager
9796 Jps
8629 NameNode
9003 SecondaryNameNode
9148 ResourceManager
~~~~

https://www.youtube.com/watch?v=ieeCyhQ2PPM

https://www.youtube.com/watch?v=wYv4lpAtcqc
