# common-mysql

Get the image:

```
docker pull mysql:8.0-debian
```
Run the image:

```
 docker run -p 0.0.0.0:3306:3306 --name betsystem-db --network=betsystem --memory 256m --memory-swap 512m -v /Users/antoniocalabretta/projects/common/common-mysql/data:/var/lib/mysql --ip 192.170.2.3 --restart always -e MYSQL_ROOT_PASSWORD="&X+5-Z3wAKkYyV" -d mysql:8.0-debian
 ```

 Notice that:

 - it's bound to all the addresses, normally should stay in its own network.
 - the volume refers to the data (it should be adapted)
 - the port is mapped, this should not be done on the contabo's server



 Ok now to move on we need to set some stuff: first of all, jump into the container as root:
 
 ```
 docker exec -it -u root  <container-id> bash
 ```

install nano:
``````
apt update
apt install nano
```

Then edit the file 
```
nano /etc/mysql/my.cnf
```

and add the line (under mysqld)

```
[mysqld] 
bind-address=0.0.0.0
```

This is to be done locally, not on the server (it would not be necessary as we don't want the server to be available to all addresses)

Then locally you are supposed to do as below (notice on linux you can go to the private ip address)

```
mysql --host 127.0.0.1 -u root -p mysql
```



