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

### Systemd
Thx @https://gist.github.com/jarek-przygodzki/735e15337a3502fea40beba27e193b04
````
sudo useradd --system --shell /bin/false node_exporter

curl -fsSL https://github.com/prometheus/node_exporter/releases/download/v1.1.2/node_exporter-1.1.2.linux-amd64.tar.gz \
  | sudo tar -zxvf - -C /usr/local/bin --strip-components=1 node_exporter-1.1.2.linux-amd64/node_exporter \
  && sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

sudo tee /etc/systemd/system/node_exporter.service <<"EOF"
[Unit]
Description=Node Exporter

[Service]
User=node_exporter
Group=node_exporter
EnvironmentFile=-/etc/sysconfig/node_exporter
ExecStart=/usr/local/bin/node_exporter $OPTIONS

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload && \
sudo systemctl start node_exporter && \
sudo systemctl status node_exporter && \
sudo systemctl enable node_exporter
````
