# Production Docker deployment for MinIO

This project enables a Docker-based deployment of [MinIO](https://min.io/), based on examples provided in [the MinIO documentation](https://docs.min.io/docs/minio-docker-quickstart-guide.html).

## Notes
- Deploys an instance of MinIO, using several containers with `docker-compose`:
  - Minio
  - Nginx
- SSL certificates are automatically generated using [docker-letsencrypt-nginx-proxy-companion](https://github.com/nginx-proxy/docker-letsencrypt-nginx-proxy-companion)

## Requirements
- A Docker instance running version `18.06.0+` of the Docker engine that supports version `3.7` or greater of the `docker-compose` file specification.
- An environment where port `80` and `443` of the host machine can be forwarded to the Nginx container for MinIO (`80` is required for Let's Encrypt certificate generation.)

## Instructions
Create the following files that contain configuration information not already defined in `docker-compose.yml`:
- `./minio-variables.env` should contain definitions for:
  - `MINIO_ACCESS_KEY` the MinIO Admin Access KEY
  - `MINIO_SECRET_KEY` the MinIO Admin Secret KEY
  - `VIRTUAL_HOST` and `LETSENCRYPT_HOST` which are the publicly accessible hostname of your MinIO instance, e.g. `minio.yourdomainhere.com`.
- `./letsencrypt-variables.env` should contain definitions for:
  - `DEFAULT_EMAIL`, an email address that the Let's Encrypt project can use to email you about important information related to your SSL certificates (e.g. expiry warnings, security issues).

Once those files are configured, you should be able to start MinIO with `docker-compose up -d`. Please note that MinIO may take a minute or two the first time it is started.
