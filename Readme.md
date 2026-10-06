# Readme.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A minimal Docker Compose deployment for [Home Assistant](https://www.home-assistant.io/). The only file is `compose.yaml`, which runs the official `ghcr.io/home-assistant/home-assistant:stable` image.

## Commands

```sh
docker compose up -d        # start Home Assistant
docker compose down         # stop it
docker compose pull && docker compose up -d   # update to latest stable image
docker logs -f homeassistant                  # follow container logs
```

## Important notes

- The config volume in `compose.yaml` is still a placeholder (`/PATH_TO_YOUR_CONFIG:/config`). It must be set to a real host path before the container will run usefully. Home Assistant's own configuration (`configuration.yaml`, etc.) lives in that mounted directory, not in this repo.
- The container uses `network_mode: host` and `privileged: true` (needed for device discovery and integrations like Bluetooth via the `/run/dbus` mount). This also means Linux-style host networking — on Windows/Docker Desktop, host networking behaves differently, which matters when testing locally.
- Timezone is set via the `TZ` environment variable (currently `Europe/Amsterdam`).
- Home Assistant's web UI is served on port 8123 of the host.
