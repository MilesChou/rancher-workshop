# Rancher Workshop

This is a simple workshop for using [Rancher][].

## Requirement

* [Docker Machine][]
* [VirtualBox][] - optional, if you want play locally.

## Workshop!

A workflow for play Rancher.

### Build

First, you may create some machine for install Rancher Server & Host:

```
docker-machine create -d virtualbox rancher-server
docker-machine create -d virtualbox rancher-host-1
docker-machine create -d virtualbox rancher-host-2
```

SSH into `rancher-server` and run Rancher Server:

```
# Check IP
docker-machine ip rancher-server

# SSH and run server
docker-machine ssh rancher-server
sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server

# See http://<SERVER_IP>:8080/ and copy the command in custom host page
```

SSH into hosts and run Rancher Agent:

```
# Check IP, it's will use at next step
docker-machine ip rancher-host-1
docker-machine ip rancher-host-2

# SSH and run agent command such as: sudo docker run -d ...
docker-machine ssh rancher-host-1
docker-machine ssh rancher-host-2
```

And now, you can see host in Rancher Page.

### Define

Here is a `docker-compose.yml` example for build wordpress:

```
wordpress:
  image: wordpress:4.6
  environment:
    WORDPRESS_DB_PASSWORD: example

mysql:
  image: mariadb:10.0
  environment:
    MYSQL_ROOT_PASSWORD: example
```

In my custom, I will add a *Load Balancer* for porting back-end service.

### Manage

Here is some examples to manage your service:

1. See STDOUT / STDERR
2. Upgrade service via Web UI
3. Upgrade service via Rancher Compose
4. Create new stack from legacy stack


[Docker Machine]: https://docs.docker.com/machine/
[Rancher]: http://rancher.com/
[VirtualBox]: https://www.virtualbox.org/
