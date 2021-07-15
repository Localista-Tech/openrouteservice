# OpenRouteService - custom by Localista Tech

This is a custom fork of OpenRouteService made by Localista Tech to be used with its applications.

The repository and its branches:

* The branch `localista` was branched from `master`. It is used as the main branch for the Localista Tech applications.

## Config before using

### OSM file

1. Download the OSM file representing the area of your interest. Store it at `openrouteservice/docker/data`.
2. At the `docker-compose.yml` file, update the argumento `OSM_FILE` with the path to your OSM file.

### `app.config`

A default for ORS by Localista Tech can be found at `openrouteservice/docker/conf-localista/app.config.localista`.
This file is copied to the Docker image when it is built, changed by what is defined at the Dockerfile and the end result stored at `openrouteservice/docker/conf/app.config`.

The `app.config.localista` file can be changed before building the Docker image, but take into account the changes made to it by the Dockerfile when building the image.

The `app.config` file can be changed after the container is created for the first time. Stop and relaunch the container and the file is loaded with the changes made to it.


## How to use

**Attention:** Everytime the GraphHopper JARs at `openrouteservice/openrouteservice/libs/` are changed, the image must be built. This is because the JARs must be installed at the local Maven repository inside the container.

To create and launch the ORS container, at `openrouteservice/docker` run:

```
$ docker-compose up -d
```

*It will build the image if it isn't available.*


To force the building of the image when creating the container, at `openrouteservice/docker` run:

```
$ docker-compose up --build -d
```

To see the logs of the container:

```
$ docker logs -f ors-app
```

To access the container:

```
$ docker exec -it ors-app /bin/bash
```

To stop and remove the container, at `openrouteservice/docker` run:

```
$ docker-compose down
```

To ensure that no wierd behavior occurs when rebuilding the image, remove dangling or unused images after removing the containers:

```
docker image prune -a
```

-----

*Original README from this point onwards.*

-----

# Openrouteservice

[![Build Status](https://travis-ci.org/GIScience/openrouteservice.svg?branch=master)](https://travis-ci.org/GIScience/openrouteservice) 
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=GIScience_openrouteservice&metric=alert_status&branch=master)](https://sonarcloud.io/dashboard?id=GIScience_openrouteservice&metric)
[![SourceSpy Dashboard](https://sourcespy.com/shield.svg)](https://sourcespy.com/github/giscienceopenrouteservice/)

The **openrouteservice API** provides global spatial services by consuming user-generated and collaboratively collected free geographic data directly from [OpenStreetMap](http://www.openstreetmap.org). It is highly customizable, performant and written in Java.

The following services are available via a HTTP interface served by Tomcat.
- **Directions** - Returns a route between two or more locations for a selected profile with customizable additional settings and instructions.
- **Isochrones** - Obtains areas of reachability from given locations.
- **Matrix** - Computes one-to-many, many-to-one or many-to-many routes for any mode of transport provided by openrouteservice.

To play around with openrouteservice you may use our [demonstration server](https://maps.openrouteservice.org) which comes with both the backend and a [frontend](https://github.com/GIScience/ors-map-client). Or simply [sign up](https://openrouteservice.org/dev/#/signup) for an API key and fire your requests against the API directly.

Please note that openrouteservice uses a forked and edited version of [graphhopper 0.13](https://github.com/GIScience/graphhopper) which can be found [here](https://github.com/GIScience/graphhopper).

[![ors client accessibility](https://user-images.githubusercontent.com/23240110/30385487-9eac96b8-98a7-11e7-9357-afd4df8fccdf.png)](https://openrouteservice.org/reach)

**Note**

- Our geocoding API is a separate service running the stack built around [**Pelias**](https://github.com/pelias/pelias).
- Our locations/API is another service which we have coined **openpoiservice** which can be found [here](https://github.com/GIScience/openpoiservice).


## Changelog/latest changes

[Openrouteservice CHANGELOG](https://github.com/GIScience/openrouteservice/blob/master/CHANGELOG.md)

## Contribute

We appreciate any kind of contribution - bug reports, new feature suggestion or improving our translations are greatly appreciated. Feel free to create an [issue](https://github.com/GIScience/openrouteservice/issues) and label it accordingly. If your issue regards the openrouteservice web-app please use the [corresponding repository](https://github.com/GIScience/ors-map-client/issues).

If you want to contribute your improvements, please follow the steps outlined in [our CONTRIBUTION guidelines](./CONTRIBUTE.md)

The [sourcespy dashboard](https://sourcespy.com/github/giscienceopenrouteservice/) provides a high level overview of the repository including technology summary, module dependencies and other components of the system.

## Installation

We recommend using Docker to install and launch the openrouteservice backend: 

```bash
cd docker && docker-compose up
```

For more details, check the [docker installation guide](https://GIScience.github.io/openrouteservice/installation/Running-with-Docker.html).

For instructions on how to [build from source](https://GIScience.github.io/openrouteservice/installation/Building-from-Source.html) or [configure](https://GIScience.github.io/openrouteservice/installation/Configuration-%28app.config%29.html), visit our [Installation and Usage Instructions](https://GIScience.github.io/openrouteservice/installation/Installation-and-Usage.html).

## Usage

Openrouteservice offers a set of endpoints for different spatial purposes. By default they will be available at

- `http://localhost:8080/ors/v2/directions`
- `http://localhost:8080/ors/v2/isochrones`
- `http://localhost:8080/ors/v2/matrix`

You can find more information in the [Installation and Usage Instructions](https://GIScience.github.io/openrouteservice/installation/Installation-and-Usage.html).

## API Documentation

For an easy and interactive way to test the api, visit our API documentation at [openrouteservice.org](https://openrouteservice.org/dev/#/api-docs).
After obtaining your key you can try out the different endpoints instantly and start firing requests.


## Questions

For questions please use our [community forum](https://ask.openrouteservice.org).

## Translations

If you notice anything wrong with translations, or you want to add a new language to the ORS instructions, we have some instructions in our [backend documentation](https://GIScience.github.io/openrouteservice/contributing/Contributing-Translations) about how you can submit an update. You can also look over at our [maps client GitHub](https://github.com/GIScience/ors-map-client/#add-language) if you want to contribute the language to there as well (adding or editing the language in the openrouteservice GitHub repo only affects the instructions - any new language also needs adding to the client).
