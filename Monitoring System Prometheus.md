# Prometheus & Grafana Mikrotik Monitoring System

## Download Prometheus


````
wget https://github.com/prometheus/prometheus/releases/download/v2.45.0/prometheus-2.45.0.linux-amd64.tar.gz
````

## Extract & Move

```
tar xzf  prometheus-2.45.0.linux-amd64.tar.gz
```

```
mv prometheus-2.45.0.linux-amd64 /etc/prometheus
```

## Systemd unit file for prometheus

```
nano /etc/systemd/system/prometheus.service
```

```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/prometheus/prometheus --config.file=/etc/prometheus/prometheus.yml
Restart=always
[Install]
WantedBy=multi-user.target
```

## Reload Systemd

```
systemctl daemon-reload
```

## Restart prometheus

```
systemctl restart prometheus
```

## Start prometheus at boot

```
systemctl enable prometheus
```

## Start prometheus at boot

```
systemctl status prometheus
```

## show ip address

```
ip
```

## Download snmp_exporter

```
wget https://github.com/prometheus/snmp_exporter/releases/download/v0.22.0/snmp_exporter-0.22.0.linux-amd64.tar.gz
```

## Extract & Move

```
tar xzf snmp_exporter-0.22.0.linux-amd64.tar.gz
```

```
mv snmp_exporter-0.22.0.linux-amd64 /etc/snmp_exporter
```

## Systemd unit file

```
nano /etc/systemd/system/snmp_exporter.service
```

```
[Unit]
Description=SNMP Exporter
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/snmp_exporter/snmp_exporter --config.file=/etc/snmp_exporter/snmp.yml
Restart=always
[Install]
WantedBy=multi-user.target
```

## Reload systemd

```
systemctl daemon-reload
```

## Restart snmp_exporter

```
systemctl restart snmp_exporter
```

## Start snmp_exporter at boot

```
systemctl enable snmp_exporter
```

## Show snmp_exporter status

```
systemctl status snmp_exporter
```

## Configure prometheus scraping

```
nano /etc/prometheus/prometheus.yml
```

```
  - job_name: 'Mikrotik'
    static_configs:
      - targets:
        - 192.168.1.2  # Mikrotik device.
    metrics_path: /snmp
    params:
      module: [mikrotik]
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9116   #ubuntuserverip
```
	
	
## Download & Install Grafana

```
sudo apt-get install -y adduser libfontconfig1
```

```
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.0.1_amd64.deb
```

```
sudo dpkg -i grafana-enterprise_10.0.1_amd64.deb
```


## Restart grafana

```
systemctl restart grafana-server
```

## Start grafana at boot

```
systemctl enable grafana-server
```

## Show grafana status

```
systemctl status grafana-server
```

## Import Dashboard

```
14857
```

