# Folders

mkdir -p /swarm/keycloak/mysql_data
mkdir -p /swarm/kong/postgres/
mkdir -p /swarm/grafana/
mkdir -p /swarm/alertmanager/data/
mkdir -p /swarm/prometheus/data/
mkdir -p /swarm/traefik/

# Config

/swarm/prometheus/alert.rules.yml
/swarm/prometheus/prometheus.yml
/swarm/alertmanager/alertmanager.yml
/swarm/traefik/traefik.toml

# Secrets

echo "admin" | docker secret create basic-auth-user -
echo "P@sw0rd" | docker secret create basic-auth-password -