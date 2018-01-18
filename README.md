# Jenkins/Traefik in Docker Swarm

## Requirements

* [Docker 17.09+](https://docker.com)

## Setup

1. `docker swarm init`
1. `mkdir -p /docker`
1. `git clone git@github.com:reynn/jenkins-traefik /docker`
1. Update `traefik/traefik.toml` and `traefik/traefik-compose.yml` to reflect your domain.
1. If not using Route53 for DNS remove it from the `traefik/traefik.toml` file
    * if you are using Route53 set values in `traefik/traefik.env` for an access token.
1. `cd /docker/jenkins && docker build -t jenkins:2.102-alpine --build-arg 2.102-alpine -f jenkins.dockerfile .`
1. `docker stack deploy -c /docker/traefik/traefik-compose.yml traefik`
1. `docker stack deploy -c /docker/jenkins/jenkins-compose.yml jenkins`
