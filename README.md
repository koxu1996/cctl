# Dockerized CCTL for Casper

Available in Docker Hub: https://hub.docker.com/r/koxu1996/casper-cctl/tags.

Couple of additional features, comparing to the upstream version:

- wildcard CORS enabled
- persistence is possible - see later section

## Casper 2.0 (RC3)

Everything you need:

```sh
docker run --rm -it -d \
    --name casper-local-2.0 \
    -p 11101:11101 -p 12101:12101 -p 13101:13101 -p 14101:14101 -p 21101:21101 -p 22101:22101 \
    koxu1996/casper-cctl:2.0-rc3
```

Wait some time until container becomes healthy:

```sh
while [ "`docker inspect -f {{.State.Health.Status}} casper-local-2.0`" != "healthy" ]; do sleep 1; echo -n "."; done
```

Then you can interact with network. Example of getting state root hash:

```sh
curl -X POST \
  --location 'http://127.0.0.1:21101/rpc' \
  --header 'Content-Type: application/json' \
  --data '{"jsonrpc": "2.0", "method": "chain_get_state_root_hash", "id": 1}'
```

### Bulding from source

Go to `release-2.0-rc3` branch.

## Casper 1.5.6

Everything you need:

```sh
docker run --rm -it -d \
    --name casper-local-1.5.6 \
    -p 11101:11101 -p 14101:14101 -p 18101:18101\
    koxu1996/casper-cctl:1.5.6
```

Wait some time until container becomes healthy:

```sh
while [ "`docker inspect -f {{.State.Health.Status}} casper-local-1.5.6`" != "healthy" ]; do sleep 1; echo -n "."; done
```

Then you can interact with network. Example of getting state root hash:

```sh
curl -X POST \
  --location 'http://127.0.0.1:11101/rpc' \
  --header 'Content-Type: application/json' \
  --data '{"jsonrpc": "2.0", "method": "chain_get_state_root_hash", "id": 1}'
```

### Bulding from source

Go to `release-1.5.6` branch.

## [Additional] Persistence

By default network state is ephemeral. If you want to persist it across reruns, start with creating shared `assets` directory:

```sh
mkdir ./assets
chmod 777 ./assets
```

Then use volume during `docker run`:

```
--volume $(pwd)/assets:/home/cctl/cctl/assets
```
