# GIS Dockerized

The goal of this project is to provide an easy way to stand up several useful GIS services for folks to learn & explore with.

## Getting Started

You will need the following installed:

- [Docker](https://www.docker.com)
- [psql](https://www.postgresguide.com/utilities/psql/) (Optional to connect to PostGIS)

Once Docker is up and running, do the following:

```bash
$ git clone git@github.com:lostmapper/gis-dockerized.git
$ cd gis-dockerized
$ docker compose up
```

This will download and run the services defined in `docker-compose.yml`.

You can shut down the containers using Control-C.

### Running Services in the Background

#### Bringing up Services in Detached Mode

To run the containers in the background, use the following command:

```bash
$ docker compose up --detach
```
#### Following Service Logs in Detached Mode

To "follow" the container logs in this mode, use the following command:

```bash
$ docker compose logs --follow
```

#### Shutting Down Services in Detached Mode

To shut down the container running in the background, use the following command:

```bash
$ docker compose down
```

## Services

Note: Wherever possible a service's data is stored on the host machine so it persists between runs.

### GeoServer

> [GeoServer](https://geoserver.org) is an open source server for sharing geospatial data.

Once the service is running you can access GeoServer at <http://localhost:8080/geoserver/web/>

The credentials for logging in as the GeoServer admin are:

- Username: `admin`
- Password: `geoserver`

GeoServers's data is stored in `data/geoserver`.

Demo data is enabled by default to facilitate learning & using the service right out of the box.

Configuration options for the GeoServer Docker image can be found at <https://github.com/geoserver/docker>.

### PostGIS

> [PostGIS](https://postgis.net) extends the capabilities of the PostgreSQL relational database by adding support for storing, indexing, and querying geospatial data.

Once the service is running you can access PostGIS at localhost:5432

To connect with psql, use the following:

```bash
psql --host=localhost --user=gis
```

The credentials for logging in are:

- Username: `gis`
- Password: `password`

PostGIS' data is stored in `data/postgis`.

Configuration options for the PostGIS Docker image can be found at https://github.com/postgis/docker-postgis
