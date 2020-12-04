# Komodo Proxy 

## What is it? 
The traefik server proxies requests to various komodo subdomains (eg. 'api.komodo.edu, relay.komodo.edu, etc) to their corresponding containers. We run traefik in `docker` mode.

## Configuring the proxy server
You will need to configure the proxy server with your own certificates. You will need to set the path to these in both the `traefik.toml` configuration file, and `docker-compose.yml`. 

### `docker-compose.yml`
```
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./traefik.toml:/traefik.toml
      # map host cert directory to container
      - < PATH TO CERT ON HOST > :< PATH TO CERT IN TRAEFIK CONTAINER >
      - < PATH TO KEY ON HOST >  :< PATH TO KEY  IN TRAEFIK CONTAINER >
```

### `traefik.toml`
```
      [[entryPoints.https.tls.certificates]]
        certFile = "< PATH TO CERT IN TRAEFIK CONTAINER >"
        keyFile =  "< PATH TO KEY  IN TRAEFIK CONTAINER >"
```