# ZOO-Project
[![Docker Image CI](https://github.com/ZOO-Project/ZOO-Project/actions/workflows/docker-image.yml/badge.svg)](https://github.com/ZOO-Project/ZOO-Project/actions/workflows/docker-image.yml)
[![DOI](https://zenodo.org/badge/353351321.svg)](https://zenodo.org/badge/latestdoi/353351321)


[ZOO-Project](http://www.zoo-project.org) ♥️ [Open Geospatial Consortium (OGC)](https://www.ogc.org/) Standards

## Summary

The **ZOO-Project** is an open source processing platform, released under MIT/X11 Licence.
It provides the polyglot **ZOO-Kernel**, a server implementation of the **Web Processing Service (WPS)** (1.0.0 and 2.0.0) and the **OGC API - Processes** standards published by the OGC. 
It contains **ZOO-Services**, a minimal set of ready-to-use services that can be used as a base to create more usefull services.
It provides the **ZOO-API**, initially only available from the JavaScript service implementation, which exposes ZOO-Kernel variables and functions to the language used to implement the service.
It contains the **ZOO-Client**, a JavaScript API which can be used from a client application to interact with a WPS server.

### ZOO-Kernel

The ZOO-Kernel is a powerful processing engine able to handle execution of service that can be implemented in various programming languages: 
 * C/C++,
 * C#,
 * Fortran,
 * Java,
 * JavaScript,
 * Python,
 * PHP,
 * Perl,
 * Ruby,
 * R
 * Node.js
 
In addition, the ZOO-Kernel can also support handling existing applications from Geographic Information System (GIS) processing engine such as:
 * [Orfeo ToolBox](https://www.orfeo-toolbox.org/)
 * [SAGA-GIS](http://saga-gis.org)

Also, the ZOO-Kernel can automatically publish data, resulting of a service execution, to [MapServer](http://mapserver.org), making the data available through Open Standards: ***Web Map Service (WMS)***, ***Web Feature Service (WFS)*** and, ***Web Coverage Service (WCS)***.

### ZOO-Services

The ZOO-Services are composed of two distinct things. First, the metadata informations which can be stored in an adhoc ZCFG format, YAML or in a dedicated database. 
Then, the ServiceProvider is the executable version of your service.
The metadata informations will define every input and output that the service will handle, their type, number and so on.
The Service Provider will obviously vary in kind from one language to another. It may be, for instance, a shared library for C language or a simple JavaScript file.

To illustrate the ease of integration of existing code as a service, the first services provided was the commonly used ***Geospatial Data Abstraction Library (GDAL)*** tools like: ogr2ogr, gdal_wrap... Also, some trivial services were implemented using the ***Computational Geometry Algorithms Library (CGAL)***.

### ZOO-API

The ZOO-API is mainly used from the JavaScript language, it gives the capability from a service to invoke other services execution implemented in other lnaguage or running from an existing GIS processing engine.
The basic ZOO-API is available for every supported programming language.

### ZOO-Client 

The ZOO-Client is a JavaScript API that can be used on client side to interact with a WPS Server.

## License

See [License](./zoo-project/LICENSE)

## Installation

Open a terminal and run the following commands:

````
git clone https://github.com/ZOO-Project/ZOO-Project.git
cd ZOO-Project
mkdir -p docker/tmp && chmod -R 777 docker
docker-compose up 
````

Then, from your favorite browser, just load the following URL: http://localhost/ and get immediate access to the 700+ ZOO-Services through WPS and OGC API - Processes depending on your preferences 🎉.


## EODHP

EODHP uses a deployment of the EOEPCA ADES component, which in turn uses ZOO-Project as the main framework. Dependencies within the ZOO project require some EODHP-specific changes.

To build and upload new builds of the EODHP ZOO image, you can use the following procedure. Ensure you replace `<version>` with the appropriate version number.

```bash
docker build --no-cache -t zoo-project:eodhp-<version> \
 --build-arg CONDA_ENV_NAME=env_zoo_calrissian \
 --build-arg PY_VER=3.10 \
 --build-arg CONDA_ENV_FILE=https://raw.githubusercontent.com/UKEODHP/eoepca-proc-service-template/master/.devcontainer/environment.yml \
 -f docker/dru/Dockerfile .
```
Tag and push to EODHP public ECR:
```bash
docker tag zoo-project:eodhp-<version> public.ecr.aws/n1b3o1k2/zoo-project-dru:eodhp-<version>

docker push public.ecr.aws/n1b3o1k2/zoo-project-dru:eodhp-<version>
```
