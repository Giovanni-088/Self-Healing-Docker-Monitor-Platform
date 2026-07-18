# cAdvisor Deployment

## Objective

Deploy cAdvisor to collect real-time Docker container metrics and expose them in the Prometheus format.

---

## Scope

This document covers:

- cAdvisor deployment
- Docker Compose configuration
- Container metrics collection
- Metrics validation
- Prometheus integration

---

## Requirements

### Software

- Ubuntu Server 26.04 LTS
- Docker Engine
- Docker Compose v2

### Network

| Service | Port |
|----------|------|
| cAdvisor | 8080 |

---

## Architecture

```
Docker Engine
      │
      ▼
  cAdvisor
      │
      ▼
 /metrics
      │
      ▼
 Prometheus
```

---

## Implementation

### Create working directory

```bash
mkdir -p docker/cadvisor
cd docker/cadvisor
```

### Docker Compose

```yaml
services:

  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor

    restart: unless-stopped

    privileged: true

    ports:
      - "8080:8080"

    devices:
      - /dev/kmsg

    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:rw
      - /sys:/sys:ro
      - /var/lib/docker:/var/lib/docker:ro
      - /dev/disk:/dev/disk:ro
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

Expected output:

```
cadvisor
STATUS Up
PORTS 8080
```

Open the web interface:

```
http://SERVER_IP:8080
```

Verify metrics endpoint:

```
http://SERVER_IP:8080/metrics
```

Expected metrics:

```
container_cpu_usage_seconds_total
container_memory_usage_bytes
container_fs_usage_bytes
container_network_receive_bytes_total
container_last_seen
```

---

## Metrics Collected

cAdvisor exports metrics including:

- CPU usage per container
- Memory consumption
- Network traffic
- Filesystem usage
- Disk I/O
- Container status
- Restart count
- Image information
- Resource limits

---

## Security Considerations

Current configuration exposes:

```
TCP 8080
```

Future improvements:

- Internal Docker network
- Reverse Proxy
- Authentication
- TLS

---

## Evidence

Validation performed:

- Container deployed successfully
- Metrics endpoint reachable
- Docker metrics available
- Ready for Prometheus scraping

Screenshot:

```
docs/assets/screenshots/cadvisor-running.png
```

---

## Problems Found

No deployment issues were encountered.

---

## Solution Applied

No corrective actions required.

---

## Result

cAdvisor successfully exports Docker container metrics in Prometheus format.

The monitoring platform is now capable of collecting container-level telemetry.

---

## Next Steps

- Deploy Prometheus
- Configure scrape targets
- Validate data collection
- Deploy Grafana
