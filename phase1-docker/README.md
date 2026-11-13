# Phase 1: Foundation - Docker

## Objective
The purpose of Phase 1 is to establish a solid foundation by applying Docker concepts to create a basic environment for containerized applications.

## Source application (provided by the course)

https://github.com/EduardUsatchev/QuakeWatch

Containerize the QuakeWatch Flask application: a Dockerfile, a Docker Compose file, and an image published to Docker Hub.

## Tasks
1. Dockerfile for the image
2. docker-compose file to run it
3. README with build and run instructions
4. Build and tag the Docker image
5. Push the Docker image to Docker Hub

## Files
| File | Purpose |
|---|---|
| [Dockerfile](Dockerfile) | Builds the image from the code in [`../app`](../app) |
| [docker-compose.yaml](docker-compose.yaml) | Builds and runs the container with one command |

## Prerequisites
- Docker installed and running
- Run all commands from the repository root (`QuakeWatch/`) unless stated otherwise

## Option 1: Build and run with Docker
```bash
docker build --network host -f phase1-docker/Dockerfile -t quakewatch:1.0 app
docker run --rm -p 5000:5000 quakewatch:1.0
```
- `-f phase1-docker/Dockerfile`: the Dockerfile location
- `app`: the build context (the application code that `COPY` uses)
- `-p 5000:5000`: host port 5000 → container port 5000 (Flask listens on 5000)

Open http://localhost:5000. Stop with `Ctrl+C`.

## Option 2: Run with Docker Compose
```bash
cd phase1-docker
docker compose up -d --build
docker compose ps
```
Open http://localhost:5000. Stop and remove the container:
```bash
docker compose down
```

## Option 3: Run the image from Docker Hub
No build needed:
```bash
docker pull yelenazamansky/quakewatch:1.0
docker run --rm -p 5000:5000 yelenazamansky/quakewatch:1.0
```
Docker Hub: https://hub.docker.com/r/yelenazamansky/quakewatch

## Tag and push (how the image was published)
```bash
docker tag quakewatch:1.0 yelenazamansky/quakewatch:1.0
docker push yelenazamansky/quakewatch:1.0
```

## Notes
**Build context**:
The Dockerfile is in `phase1-docker/`, but the code is in `app/`.
That's why the build uses `-f phase1-docker/Dockerfile` with `app` as the context,
and Compose uses `context: ../app` with `dockerfile: ../phase1-docker/Dockerfile`.

**`--network host` (WSL only)**:
In my WSL environment, containers created during the build can't reach the DNS server,
so `pip install` fails. Building with host networking fixes it.
On a regular Linux or Docker Desktop setup this flag isn't needed.

**`restart: always`**:
The Compose container restarts automatically, also after a reboot.
Run `docker compose down` when you're done.