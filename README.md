# Florida HA Lite

Lightweight Home Assistant Container setup for a MacBook-hosted Florida room
automation.

The current focus is a Frigidaire bathroom dehumidifier. Home Assistant watches
the unit's own humidity sensor and turns the dehumidifier on or off
automatically.

## Function

- Run Home Assistant locally with Docker Desktop on macOS.
- Keep Home Assistant lightweight with CPU, memory, swap, and log limits.
- Control a Frigidaire dehumidifier through Home Assistant.
- Use the dehumidifier humidity sensor as the automation input.
- Turn the dehumidifier on when humidity rises.
- Turn the dehumidifier off when humidity drops.
- Keep all private Home Assistant state out of GitHub.

## Automation Behavior

```text
Bathroom humidity > 55% for 2 minutes
-> turn on humidifier.bathroom_dehumid
-> set target humidity to 35%

Bathroom humidity < 45% for 2 minutes
-> turn off humidifier.bathroom_dehumid
```

The automation is in:

```text
homeassistant/automations.yaml
```

## Repository Layout

```text
.
├── README.md
├── CHANGELOG.md
├── LICENSE
├── docs
│   ├── ARCHITECTURE.md
│   ├── OPERATIONS.md
│   └── SECURITY.md
└── homeassistant
    ├── compose.yaml
    ├── configuration.yaml
    ├── automations.yaml
    ├── scripts.yaml
    └── scenes.yaml
```

## Quick Start

Install Docker Desktop, then run:

```bash
cd homeassistant
docker compose up -d
```

Open:

```text
http://127.0.0.1:8123
```

If `docker` is not available in the shell PATH on macOS, use Docker Desktop's
bundled binary:

```bash
/Applications/Docker.app/Contents/Resources/bin/docker compose up -d
```

## Required Home Assistant Integration

This repo assumes a Frigidaire integration that exposes:

```text
humidifier.bathroom_dehumid
sensor.bathroom_dehumid_humidity
```

If your entity IDs differ, update `homeassistant/automations.yaml`.

## What Is Intentionally Not Included

The live Home Assistant config contains private state and credentials. This
repo intentionally does not include:

```text
.storage/
secrets.yaml
home-assistant_v2.db*
*.log
backups/
token/cache files
```

See [Security Notes](docs/SECURITY.md) before committing anything copied from a
live Home Assistant instance.

## Docs

- [Architecture](docs/ARCHITECTURE.md)
- [Operations](docs/OPERATIONS.md)
- [Security Notes](docs/SECURITY.md)
- [Changelog](CHANGELOG.md)

