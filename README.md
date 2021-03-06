# Prometheus "NULL" Remote Storage Adapter to create your own!

[![Build on Linux](https://github.com/ledyba/prometheus_null_adapter/workflows/Build%20on%20Linux/badge.svg)](https://github.com/ledyba/prometheus_null_adapter/actions?query=workflow%3A%22Build+on+Linux%22)
[![Build on macOS](https://github.com/ledyba/prometheus_null_adapter/workflows/Build%20on%20macOS/badge.svg)](https://github.com/ledyba/prometheus_null_adapter/actions?query=workflow%3A%22Build+on+macOS%22)
[![Build on Windows](https://github.com/ledyba/prometheus_null_adapter/workflows/Build%20on%20Windows/badge.svg)](https://github.com/ledyba/prometheus_null_adapter/actions?query=workflow%3A%22Build+on+Windows%22)  
[![Build single binary on Linux](https://github.com/ledyba/prometheus_null_adapter/workflows/Build%20single%20binary%20on%20Linux/badge.svg)](https://github.com/ledyba/prometheus_null_adapter/actions?query=workflow%3A%22Build+single+binary+on+Linux%22)

Prometheus remote storage adapter, which stores timeseries data into RDBMS.

## Building and running

### with Cargo

```bash
cargo build --release
```

then run,

```bash
target/release/prometheus_null_adapter web \
  --listen '0.0.0.0:8080'
```

### with Docker

Write a docker-compose.yml like:

```yaml
---
version: '3.7'

services:
  prometheus_null_adapter:
    container_name: prometheus_null_adapter
    hostname: prometheus_null_adapter
    image: prometheus_null_adapter
    build:
      context: ./
    restart: always
    command: "web --listen '0.0.0.0:8080'"
```

then,

```bash
docker-comopse build # It takes long time. Be patient....
docker-comopse up -d
```

## Using from Prometheus

Write these line to `/etc/prometheus/config.yml`

```yaml
remote_write:
  - url: 'http://<hostname>:8080/write'
remote_read:
  - url: 'http://<hostname>:8080/read'
```
