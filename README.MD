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
docker network create -d overlay --label openfaas=true function_net
docker network create -d overlay db_net

# Order

## Traefik

docker stack deploy -c docker-compose.yml traefik --with-registry-auth

User: admin
Password: senha123

http://traefik.docker.internal/dashboard/#/

## Prometheus

docker stack deploy -c docker-compose.yml prometheus --with-registry-auth