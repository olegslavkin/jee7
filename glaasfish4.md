## Setup Glassfish 4

### 1. Start domain
```
$ cd /opt/glassfish4/bin
$ ./asadmin start-domain
```
### 2. Change admin password
```
$ ./asadmin change-admin-password
$ ./asadmin enable-secure-admin
```
### 3. Restart domain
```
$ ./asadmin restart-domain
```
### 4. Open http://x.x.x.x:8080 and https://x.x.x.x:4848
