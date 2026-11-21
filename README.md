# pocketbase-docker-compose

Quickly set up a local PocketBase environment using Docker Compose.

## Running locally

To start the PocketBase environment locally, run the following command:

```sh
docker compose up -d
```

This will start the necessary services in detached mode. PocketBase listens on `http://127.0.0.1:8090` only; put a reverse proxy in front of it to expose it elsewhere.

The container runs as a non-root user (uid/gid 1000 by default). If your host user is different, create the `pb/` directories first and pass your ids so the bind mounts are writable:

```sh
mkdir -p pb/data pb/public pb/hooks pb/migrations
PB_UID=$(id -u) PB_GID=$(id -g) docker compose up -d
```

## PocketBase version

The version is set by `PB_VERSION` and `PB_RELEASE_ID` in `Dockerfile.pocketbase`. A daily workflow opens a pull request when a new release is published. The image build checks the download against the release's `checksums.txt`. Back up `pb/` before upgrading, because new versions can run data migrations on start.

## PocketBase files

All PocketBase files, including the database and configuration files, are stored in the `pb/` directory. This directory is mounted as a volume in the Docker Compose setup, ensuring that your data persists across container restarts.

| Directory | Mounted at | Purpose |
| --- | --- | --- |
| `pb/data` | `/pb/pb_data` | database and uploaded files |
| `pb/public` | `/pb/pb_public` | static files served by PocketBase |
| `pb/hooks` | `/pb/pb_hooks` | JavaScript hooks |
| `pb/migrations` | `/pb/pb_migrations` | schema migrations, so changes made in the admin UI can be committed |

`pb/` is gitignored. Back it up regularly (at minimum `pb/data`) to prevent data loss.
