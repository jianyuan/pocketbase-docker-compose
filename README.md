# pocketbase-docker-compose

Quickly set up a local PocketBase environment using Docker Compose.

## Running locally

To start the PocketBase environment locally, run the following command:

```sh
docker compose up -d
```

This will start the necessary services in detached mode.

## PocketBase files

All PocketBase files, including the database and configuration files, are stored in the `pb/` directory. This directory is mounted as a volume in the Docker Compose setup, ensuring that your data persists across container restarts.

Make sure to back up this directory regularly to prevent data loss.
