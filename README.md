# Lego Vault

Vaultwarden and Caddy setup.

## Start the service

Use `docker compose up -d`

## Port forwarding

Forwarding port 80 is necessary for the ACME HTTP-01 challenge to work (Caddy uses Let's Encrypt certbot).

## Temporarily allowing signups

Edit `docker-compose.yml` and change the environment variable `SIGNUPS_ALLOWED` from `false` to `true`.

Restart docker compose with `docker compose down && docker compose up -d`.

Do not commit this change to the git repo.

When done creating accounts issue:

```sh
git reset --hard
docker compose down
docker compose up -d
```

# Udating when using Docker Compose

docker compose pull
docker compose up -d
