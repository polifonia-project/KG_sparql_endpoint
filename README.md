# KG SPARQL ENDPOINT

This repository contains a docker file to deploy the Polifonia KG Sparql Endpoint.

Polifonia KG triples are collected by etl services such as [KG data transformation](https://github.com/polifonia-project/KG_data_transformation).

Data are modelled according to the [Polifonia Ontology Network](https://github.com/polifonia-project/ON).

To deploy the Polifonia KG Sparql Endpoint as a docker service you need [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/) installed on your machine.
Refer to official documentation for installation.


## Deploy

The following instructions show how to deploy the service.

#### Build the service

First of all download this codebase and cd to the downloaded folder:

`git clone https://github.com/polifonia-project/kg_sparql_endpoint.git && cd ./kg_sparql_endpoint`

Build command:

`docker-compose build`

Launch the service (the `-d` flag will detach the process from current terminal):

`docker-compose up -d`

#### Stop the service

`docker-compose down`

#### Rebuild the service

Delete the volume with old triples and DB data:


`docker volume rm kg_sparql_endpoint_polifonia-kg`

Rebuild 


`docker-compose up --build --no-cache`

Note: `--no-cache` flag is needed to download again remote KG triples and ontologies, in case a new version is uploaded.


## Environment

You can pass environment variables through an environment file.
Just create a file named `.env` in the root folder of this project.

Valid env variables are:

Port where sparql endpoint is listening for requests:
- `POLIFONIA_SP_ENDP_PORT=<port-number,default=8891>`

Password for the sparql endpoint management console:
- `POLIFONIA_SP_ENDP_PWD=<password,default=password>`

See `.env.example` file for an example env file.


If you deploy Polifonia KG Sparql Endpoint locally you can access it at: `localhost:<port-number>/sparql`
