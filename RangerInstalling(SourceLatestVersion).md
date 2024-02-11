# Installing And Configuring *Ranger*  version 0.5 from [ApacheRangerLatestVersion-OfficialApacheWebsite](https://ranger.apache.org/quick_start_guide.html)

## Some Prerequistes before we actually install *Ranger*  

### Installing Maven

You need first to switch to root user or *sudo* them  

``` bash
su - tariq # This my username in sudo group

# Download maven latest distribution tar from apache maven site 
# This the appropriate version of maven that is suitble for JDK/JAVA 7
wget -P ~/Downloads https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz

sudo mkdir /usr/local/maven

# Unzip the file
tar -xvf ~/Downloads/apache-maven-3.8.8-bin.tar.gz -C /usr/local/maven # This is going to *tar* the file into /usr/local

# Set some env variables
export M2_HOME=/usr/local/maven/apache-maven-3.8.8
export M2=$M2_HOME/bin
export PATH=$M2:$PATH

# Just to make the changes permenant
echo 'export M2_HOME=/usr/local/maven/apache-maven-3.8.8' >> ~/.bashrc
echo 'export M2=$M2_HOME/bin' >> ~/.bashrc
echo 'export PATH=$M2:$PATH' >> ~/.bashrc
source ~/.bashrc 
  
# Now to test your install of Maven, enter the following command
mvn -version
```
*OR*  

``` bash   
sudo apt update
sudo apt install maven 
```  

### Install GIT  
``` bash  
sudo apt install git
```

### Install MySQL  

1-  First you need to install MySQL
``` bash
sudo apt install mysql-server  
sudo service mysql status # The MySQL service should start automaticlly verify by this command
sudo systemctl start mysql.service # If not, This will start the my sql service   
```  
2-  Configure security installation

This following will prompt you to:
  - Set a root password (if not already during installation)
  - Remove anonmous users  
  - Disallow root login remotely  
  - Remove the test database
  - Reload privilege tables      

And I choose *No* for testing purposes!
``` bash
sudo mysql_secure_installation
```  

3-  Download the MySQL JDBC, and then untarit, then finally copy the .jar file to a common location where everyone be abel to access it.

``` bash  
# This will download the appropriate MySQL JDBC packge for Ubuntu 20.04 LTS
wget -P ~/Downloads https://downloads.mysql.com/archives/get/p/3/file/mysql-connector-j_8.0.33-1ubuntu20.04_all.deb
sudo dpkg -i ~/Downloads/mysql-connector-j_8.0.33-1ubuntu20.04_all.deb # This will install the .deb package
```  

## Install And Build Ranger from the source  

1-  Clone the ranger source code  
Ranger is still an incubater porject !, so that means there not yet compiled version of it (.exe), so we have to build Ranger using the source code!  
``` bash  
mkdir ~/dev  
cd ~/dev  
git clone https://github.com/apache/range
cd ranger  
```

2-  Add some evn variables to `.bashrc`  
``` bash    
export JAVA_HOME=$(readlink -f `which java` | sed "s:/bin/java::")
export PATH=$JAVA_HOME/bin:$PATH

# This will make the JAVA_HOME and PATH permenant ! (because ~/.bashrc runs on every boot)
echo 'export JAVA_HOME=$(readlink -f `which java` | sed "s:/bin/java::")' >> ~/.bashrc
echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc
```

3-  Build the source code
``` bash    
cd ~/dev/ranger  
mvn -Pall clean  
mvn -Pall -DskipTests=false clean compile package install  
```  