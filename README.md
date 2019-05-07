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




https://www.youtube.com/watch?v=ieeCyhQ2PPM
