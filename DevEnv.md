# Ubuntu 14.04.1 Server LTS
```
$ uname -a
Linux javaee7 3.13.0-32-generic #57-Ubuntu SMP Tue Jul 15 03:51:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
```

```
$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 14.04.1 LTS
Release:	14.04
Codename:	trusty
```

# Install Oracle JDK 8
```
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```

# Verify Java Version
```
$ java -version
java version "1.8.0_25"
Java(TM) SE Runtime Environment (build 1.8.0_25-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.25-b02, mixed mode)
```
# Download Oracle Java EE 7 SDK
```
$ wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/java_ee_sdk/7u3/java_ee_sdk-7u1.zip
```
# Unzip java_ee_sdk-7u1.zip
```
$ sudo unzip -d /opt/ java_ee_sdk-7u1.zip
```
# Install maven, git
```
$ sudo apt-get install maven git
```

# Oracle Java EE 7 Tutorial
```
$ wget http://docs.oracle.com/javaee/7/tutorial/doc/javaeetutorial7.pdf
```
