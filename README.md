# Quick Start
```sh
git clone https://github.com/matthew-hollick/graphite-clickhouse-tldr.git
cd graphite-clickhouse-tldr
pushd dockerfiles/carbonapi
docker build -t carbonapi .
popd
docker-compose up
```
Open http://127.0.0.1:3000 in browser to access Grafana

Username and Password are `admin`

Open http://127.0.0.1 in browser to access graphite-web

## Grafana Datasources

In grafana UI add:

### Graphite-web

http://graphite-web

### Carbonapi

http://carbonapi:8080

## Mapped Ports

Host | Container | Service
---- | --------- | -------------------------------------------------------------------------------------------------------------------
  80 |        80 | [nginx](https://www.nginx.com/resources/admin-guide/)
2003 |      2003 | [carbon receiver - plaintext](http://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-plaintext-protocol)
2004 |      2004 | [carbon receiver - pickle](http://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-pickle-protocol)
2006 |      2006 | [carbon receiver - prometheus remote write](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#%3Cremote_write%3E)
3000 |      3000 | Grafana

## Loading with haggar

Where <<IP_ADDRESS>> is your local machine address (127.0.0.1 does not work on macs)

```
docker run -it egaillardon/haggar -carbon <<IP_ADRESS>>:2003 -agents 10 -metrics 100
```

# TODO
Add Grafana datasources to be imported on boot.
