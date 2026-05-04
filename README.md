# Lego Vault

Vaultwarden and Caddy docker rootless setup with DuckDNS plugin.

## IP Updater via cron

With Docker rootless is difficult for the IP updater image/container to get the host IP even with "host" network mode.

So it's better to just add a cronjob.

First test the command line:

`curl https://www.duckdns.org/update/toximaxi/{$TOKEN}/$(curl -s -6 icanhazip.com)`

`crontab -e`

```cron
*/5 * * * * curl https://www.duckdns.org/update/toximaxi/{$TOKEN}/$(curl -s -6 icanhazip.com) > /dev/null 2>&1
```

## Start/restart the service

Use `docker compose down && docker compose up -d --build`

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
