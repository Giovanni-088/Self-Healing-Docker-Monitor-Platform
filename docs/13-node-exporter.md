# Node Exporter Deployment

## Objective

Deploy Node Exporter as the first telemetry component of the monitoring platform to expose host-level metrics for Prometheus.

---

## Scope

This document covers:

- Node Exporter deployment
- Docker Compose configuration
- Network exposure
- Service validation
- Initial metrics verification

---

## Requirements

### Software

- Ubuntu Server 26.04 LTS
- Docker Engine
- Docker Compose v2

### Network

Port required:

| Service | Port |
|----------|------|
| Node Exporter | 9100 |

---

## Architecture

```
Ubuntu Server
│
├── Docker Engine
│
└── Node Exporter
        │
        ▼
 Exposes /metrics
        │
        ▼
 Prometheus
```

---

## Implementation

### Create working directory

```bash
mkdir -p docker/node-exporter
cd docker/node-exporter
```

### Docker Compose

```yaml
services:

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter

    restart: unless-stopped

    ports:
      - "9100:9100"

    pid: host

    volumes:
      - /:/host:ro,rslave

    command:
      - "--path.rootfs=/host"
```

### Deploy

```bash
docker compose up -d
```

---

## Verification

Verify the container:

```bash
docker ps
```

Expected:

```
node-exporter
STATUS Up
PORTS 9100
```

Verify metrics endpoint:

```
http://SERVER_IP:9100/metrics
```

Expected result:

- HTTP 200 OK
- Thousands of Prometheus metrics displayed

Example metrics:

```
node_cpu_seconds_total
node_memory_MemAvailable_bytes
node_disk_read_bytes_total
node_network_receive_bytes_total
```

---

## Metrics Collected

Node Exporter provides metrics including:

- CPU usage
- Memory usage
- Disk usage
- Filesystem information
- Network traffic
- Load Average
- System uptime
- Running processes
- File descriptors
- System temperature (if available)

---

## Security Considerations

Current configuration exposes:

```
TCP 9100
```

The service is intended to be accessed only by Prometheus.

Future improvements:

- Reverse Proxy
- Authentication
- Internal monitoring network
- TLS encryption

---

## Evidence

Validation performed:

- Docker container running successfully
- Metrics endpoint accessible
- Docker restart policy configured
- Ready for Prometheus integration

Screenshot to add:

```
docs/assets/screenshots/node-exporter-running.png
```

---

## Problems Found

No issues encountered during deployment.

Docker image was downloaded successfully and the service started on the first attempt.

---

## Solution Applied

No corrective actions required.

---

## Result

Node Exporter is operational and exporting host metrics through the Prometheus exposition format.

The server is now ready to be scraped by Prometheus.

---

## Next Steps

- Deploy cAdvisor
- Deploy Prometheus
- Configure scrape targets
- Build Grafana dashboards
