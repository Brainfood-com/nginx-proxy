Brainfood Nginx Proxy
=====================

Getting Started
---------------

* Install docker
* Install docker-compose
* git clone https://github.com/Brainfood-com/nginx-proxy.git
* cd nginx-proxy
* docker network create nginx
* docker-compose up -d

Attaching backend webservers
----------------------------

To attach a backend webserver to this proxy, it needs to be added to the
global nginx overlay network.  In the backend docker-compose.yml:

```yaml
version: 2
networks:
  default:
  nginx:
    external:
      name: nginx

services:
  my-vhost:
    image: my-image
    networks:
      - default
      - nginx
    ports:
      - 8080
    environment:
      - VIRTUAL_PORT=8080
      - VIRTUAL_HOST=my-vhost.localhost

```

Origin
------

This project is based on jwilder/nginx-proxy, but designed to not have any
internal virtual hosts.  Instead, those are connected via an external overlay
network.  This project is meant to be installed once on a host.

The original jwilder repository is MIT licensed, so this one is as well.
