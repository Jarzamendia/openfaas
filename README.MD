# Folders

mkdir -p /swarm/keycloak/mysql_data
mkdir -p /swarm/kong/postgres/
mkdir -p /swarm/grafana/
mkdir -p /swarm/alertmanager/data/
mkdir -p /swarm/prometheus/data/
mkdir -p /swarm/traefik/
mkdir -p /swarm/portainer/data

# Config

/swarm/prometheus/alert.rules.yml
/swarm/prometheus/prometheus.yml
/swarm/alertmanager/alertmanager.yml
/swarm/traefik/traefik.toml

# Secrets

echo "admin" | docker secret create basic-auth-user -
echo "P@sw0rd" | docker secret create basic-auth-password -

# Networks

docker network create -d overlay agent_net
docker network create -d overlay proxy_net
docker network create -d overlay --label openfaas=true --attachable	 function_net
docker network create -d overlay db_net

# Order

## Traefik

docker stack deploy -c docker-compose.yml traefik --with-registry-auth

User: admin
Password: senha123

http://traefik.docker.internal/dashboard/#/

## Portainer

docker stack deploy -c docker-compose.yml portainer --with-registry-auth

http://portainer.docker.internal

## Prometheus

docker stack deploy -c docker-compose.yml prometheus --with-registry-auth

http://grafana.docker.internal
http://prometheus.docker.internal
http://alertmanager.docker.internal

## OpenFaas

docker stack deploy -c docker-compose.yml openfaas --with-registry-auth

http://gateway.docker.internal

## Kong

docker stack deploy -c docker-compose.yml kong --with-registry-auth