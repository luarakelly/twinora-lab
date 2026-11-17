# Twinora Lab

Twinora Lab is a local-first digital twin for plant rooms: scan a room, find and name its equipment, link it
to equipment data and explore it in the browser.

This repository contains the **ready-to-run Docker image** and user documentation. The source code is
private.

## Run it

You need [Docker](https://docs.docker.com/get-docker/). Then:

```sh
docker run -p 8000:8000 -v twinora-data:/data ghcr.io/luarakelly/twinora-lab:latest
```

Open http://localhost:8000.

Or, after cloning this repository:

```sh
docker compose up
```

## Your data

Everything you create (the database, uploaded scans and videos) is stored in the Docker volume
`twinora-data`, mounted at `/data`. It survives restarts and image updates. The image itself contains no
data.

| Task | Command |
|---|---|
| Update to the newest version | `docker pull ghcr.io/luarakelly/twinora-lab:latest`, then start it again |
| Use a specific version | replace `latest` with a version, e.g. `0.1.0` |
| Back up your data | `docker run --rm -v twinora-data:/data -v "$PWD":/backup alpine tar czf /backup/twinora-data.tgz -C /data .` |
| Start from scratch | `docker volume rm twinora-data` (deletes all your data) |

## What works today

- A fresh start opens the **Valmet** facility.
- Facilities: choose a facility from the sidebar (searchable), with its Overview, Areas and Assistant
  sections.
- Server status at the bottom of the sidebar.

Areas (list, create, upload a scan, follow processing) arrive in the next versions.

## Configuration

| Variable | Default | Meaning |
|---|---|---|
| `TWINORA_MAX_UPLOAD_BYTES` | `2147483648` (2 GiB) | largest upload |

Pass it with `-e`, e.g. `docker run -e TWINORA_MAX_UPLOAD_BYTES=1073741824 ...`.
