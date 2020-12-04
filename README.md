# Komodo Proxy 

## What is it? 
The traefik proxy server routes requests for various subdomains (eg. 'api.komodo.edu', 'relay.komodo.edu', etc) to their corresponding docker containers.

## Configuring the proxy server
You will need to configure the proxy server with your own certificates. You will need to set the correct paths both the `traefik.toml` configuration file, and `docker-compose.yml`. 

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