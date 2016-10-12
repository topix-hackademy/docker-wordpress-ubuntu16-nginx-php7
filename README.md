# docker-wordpress-ubuntu16-nginx-php7

A Dockerfile that installs the latest wordpress on Ubuntu 16.04 with nginx 1.10.0, php-fpm7.0, php7.0 APC User Cache and openssh. You can also handle the services using supervisord.
Based on [this](https://hub.docker.com/r/thomasvan/docker-wordpress-ubuntu16-nginx-php7/).

## Installation

The easiest way get up and running with this docker container is to pull the latest stable version from the [Docker Hub Registry](https://hub.docker.com/r/alexcomu/docker-wordpress-ubuntu16-nginx-php7):

```bash
$ docker pull alexcomu/docker-wordpress-ubuntu16-nginx-php7:latest
```

If you'd like to build the image yourself:

```bash
$ git clone https://github.com/topix-hackademy/docker-wordpress-ubuntu16-nginx-php7.git
$ cd docker-wordpress-ubuntu16-nginx-php7
$ sudo docker build -t="alexcomu/docker-wordpress-ubuntu16-nginx-php7" .
```

## Usage

The -p 80:80 maps the internal docker port 80 to the outside port 80 of the host machine. The other -p sets up sshd on port 2222.
The -p 9011:9011 is using for supervisord, listing out all services status.
```bash
$ sudo docker run -p 7000:22 -p 8000:80 --name WORDPRESS-1 -h WORDPRESS-1 -d alexcomu/docker-wordpress-ubuntu16-nginx-php7:latest
```

Start your newly created container, named *docker-name*.

```
$ sudo docker start WORDPRESS-1
```

After starting the container docker-wordpress-nginx-ssh checks to see if it has started and the port mapping is correct.  This will also report the port mapping between the docker container and the host machine.

```
$ sudo docker ps

3306/tcp, 0.0.0.0:9011->9011/tcp, 0.0.0.0:2222->22/tcp, 0.0.0.0:8080->80/tcp
```

You can then visit the following URL in a browser on your host machine to get started:

```
http://127.0.0.1:8080
```

You can start/stop/restart and view the error logs of nginx and php-fpm services:
```
http://127.0.0.1:9011
```

You can also SSH to your container on 127.0.0.1:2222. The default password is *wordpress*, and can also be found in .ssh-default-pass.

```
$ ssh -p 2222 wordpress@127.0.0.1
# To drop into root
$ sudo -s
```

Now that you've got SSH access, you can setup your FTP client the same way, or the SFTP Sublime Text plugin, for easy access to files.

To get the MySQL's password, check the top of the docker container logs for it:

```
$ docker logs <container-id>
```
or ssh to your container and view those files:
```
$ cat /wordpress-db-pw.txt
$ cat /mysql-root-pw.txt
```
