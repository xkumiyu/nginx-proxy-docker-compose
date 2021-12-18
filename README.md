# Nginx Proxy Docker Compose Examples

[nginx-proxy](https://github.com/nginx-proxy/nginx-proxy)

## Simple

```sh
cd simple
docker compose up
```

```sh
curl -H Host:whoami.local localhost
```

Example output:

```text
I'm 1ca17e445895
```

## Multiple Hosts

```sh
cd multiple-hosts
docker compose up
```

```sh
curl -H Host:whoami.local localhost
curl 127.0.0.1.sslip.io
```

## Basic Authentication

Place htpasswd file as `$VIRTUAL_HOST`.

```sh
cd basic-auth
echo "user:$(openssl passwd -apr1 pass)" > whoami.local
docker compose up
```

```sh
curl -H Host:whoami.local -u user:pass localhost
```

## SSL using ACME CA

Requirements

- allow access to port 80 from internet
  - required for HTTP authentication when issuing certificates
- own a domain
  - if you have a global IP, you can use [sslip.io](https://sslip.io/).

```sh
cd ssl
```

```sh
echo "HOST=$YOUR_DOMAIN" > .env
# when using sslip
echo "HOST=$YOUR_IP.sslip.io" > .env
```

```sh
docker compose up
```
