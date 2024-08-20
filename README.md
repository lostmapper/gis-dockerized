# GIS Dockerized

The goal of this project is to provide an easy way to stand up several useful GIS services for folks to learn & explore with.

## Getting Started

You will need the following installed:

- [Docker](https://www.docker.com)

Once Docker is up and running, do the following:

```bash
$ git clone git@github.com:lostmapper/gis-dockerized.git
$ cd gis-dockerized
$ docker compose up
```

This will download and run the services defined in `docker-compose.yml`.

You can shut down the containers using Control-C.

## Included Services

| Service   | Name        | URL                                    | Username | Password   | Data Location    |
|-----------|-------------|----------------------------------------|----------|------------|------------------|
| GeoServer | `geoserver` | <http://localhost:8080/geoserver/web/> | `gis`    | `password` | `data/geoserver` |
| MapStore  | `mapstore`  | <http://localhost:8081/mapstore/>      | `admin`  | `admin`    | PostGIS          |
| PostGIS   | `postgis`   | N/A                                    | `gis`    | `password` | `data/postgis`   |
| Solr      | `solr`      | <http://localhost:8983/solr/>          | N/A      | N/A        | `data/solr`      |

Note: Wherever possible a service's data is stored on the host machine so it persists between runs.


### GeoServer (geoserver)

> [GeoServer](https://geoserver.org) is an open source server for sharing geospatial data.

Once the service is running you can access GeoServer at <http://localhost:8080/geoserver/web/>

The REST API is available at <http://localhost:8080/geoserver/rest/>

#### Credentials

The credentials for logging in as the GeoServer admin are:

- Username: `gis`
- Password: `password`

#### Data

GeoServers's data is stored in `data/geoserver`.

Demo data is enabled by default to facilitate learning & using the service right out of the box.

#### Configuration

Configuration options for the GeoServer Docker image can be found at <https://github.com/geoserver/docker>.

### MapStore (mapstore)

> [MapStore](https://docs.mapstore.geosolutionsgroup.com/) is a highly modular Open Source WebGIS framework to create, manage and securely share maps and mashups.

Once the service is running you can access MapStore at <http://localhost:8081/mapstore/>

#### Credentials

The credentials for logging in as the MapStore admin are:

- Username: `admin`
- Password: `admin`

#### Data

MapStore's data is stored in the PostGIS database describe below.

### PostGIS (postgis)

> [PostGIS](https://postgis.net) extends the capabilities of the PostgreSQL relational database by adding support for storing, indexing, and querying geospatial data.

Once the service is running you can access PostGIS at `localhost` on port `5432`

To connect with [psql](https://www.postgresql.org/docs/current/app-psql.html), use the following:

```bash
psql --host=localhost --user=gis
```

#### Credentials

The credentials for logging in are:

- Username: `gis`
- Password: `password`

#### Data

PostGIS data is stored in `data/postgis`.

#### Configuration

Configuration options for the PostGIS Docker image can be found at https://github.com/postgis/docker-postgis

### Solr (solr)

> [Solr](https://solr.apache.org) is the popular, blazing-fast, open source enterprise search platform built on Apache Lucene

Once the service is running you can access Solr at <http://localhost:8983/solr/>

#### Data

Solr data is stored in `data/solr`.

#### Configuration

The Solr services is configured with a core named `blacklight-core` to be used with an instance of [GeoBlacklight](https://geoblacklight.org)

The `blacklight-core` configuration in the `solr_conf` directory is a copy of the [`solr/conf` directory in the 4.4.0 release of GeoBlacklight](https://github.com/geoblacklight/geoblacklight/tree/v4.4.0/solr/conf).

## Additional Notes

### Running Services in the Background

#### Bringing up Services in Detached Mode

To run the containers in the background, use the following command:

```bash
$ docker compose up --detach
```
#### Following Service Logs in Detached Mode

To follow/tail the container logs in this mode, use the following command:

```bash
$ docker compose logs --follow
```

#### Shutting Down Services in Detached Mode

To shut down the container running in the background, use the following command:

```bash
$ docker compose down
```

### Running Individual Services

If you only need to run a single service provided by this project you can specify its name after the `up` command. For example, to just run Solr use the following command:

```bash
$ docker compose up solr
```

This can also be combined with the `--detach` option per above.

#### Running MapStore

MapStore requires PostGIS to persist its data. To run just those two services, use the following command:

```bash
$ docker compose up mapstore postgis
```
