# iot-stack
This is an easily setupable dockerized Iot stack based on RabbitMQ message queue, with monitoring and security features.
This stack will give you a functional rabbitmq with secure mqtt endpoint and grafana metrics.

![Architecture diagram](architecture.png)

## Before start
This stack is based on [Docker technology](https://docs.docker.com/). That means you can start or stop these systems anytime you want, or run it on an other system and the same setup will start.

## How to start / setup
Before start the default passwords/domains can set if you wish.
The default password is password and the domain is localhost.
1. First compose up the Traefik reverse-proxy. After starting it, you should be able to check it's status via the ui (with authentication admin/password) on https://traefik-ui.localhost ![traefikui](traefikui.png)

        docker-compose -f traefik/docker-compose.yml up -d

2. (optional) Then start the Portainer if you wish. After starting, you should be able to access it on https://portainer.localhost by default and it will ask you to create the default user.

        docker-compose -f portainer/docker-compose.yml up -d
        
3. After, the Prometheus stack and Rabbitmq stacks can start as well. You should be able to access them on https://rabbitmq.localhost (guest/guest) and https://grafana.localhost (admin/password)

        docker-compose -f rabbitmq/docker-compose.yml up -d
        docker-compose -f prometheus/docker-compose.yml up -d
        
4. Connect Grafana with Prometheus ![prometheusdatasource](prometheusdatasource.png). You can now install dashboards, or create your own if you wish. You get metrics from the Traefik, RabbitMQ and the host system (via [Node-Exporter](https://hub.docker.com/r/prom/node-exporter)).

5. Install dashboards in grafana. On Grafana after login Dashboard->Import ![traefikdb2](traefikdb2.png)
![traefikdb1](traefikdb1.png)

## TODOs
- [ ] Implement Elastic stack with Kibana dashboard. That will give you ability to create dashboards from data you sent over rabbitmq (mqtt as well of course). Till I integrate Elastic to this stack, you can use this cool repo: https://github.com/deviantony/docker-elk
- [ ] Make Grafana datasource setup autonomus.