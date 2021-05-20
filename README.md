# Prometheus Setup

## Docker Compose

### Start up
````
docker-compose up -d
````

### Logs
````
docker-compose logs -f
````

### Stop
````
docker-compose down
````

## Node Exporter Setup
````
wget https://github.com/prometheus/node_exporter/releases/download/v*/node_exporter-*.*-amd64.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
./node_exporter
````

