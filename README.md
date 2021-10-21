# KG SPARQL ENDPOINT

This repository contains a docker file to deploy the Polifonia KG Sparql Endpoint.

Polifonia KG triples are collected by etl services such as [KG data transformation](https://github.com/polifonia-project/KG_data_transformation).

Data are modelled according to the [Polifonia Ontology Network](https://github.com/polifonia-project/ON).

To deploy the Polifonia KG Sparql Endpoint as a docker service you need [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/) installed on your machine.
Refer to official documentation for installation.

A live version of the sparql endpoint can be found at: https://arco.istc.cnr.it/polifonia/sparql

## Browse the Graph

You can look at the [transformations](https://github.com/polifonia-project/KG_data_transformation#transformations) producing the KG to have an idea of data shape. Transformations are done in pure SPARQL and in the `CONSTRUCT` section you can find the pattern modelling triples.

E.g. 

```
CONSTRUCT { 

    # Recording
    ?recordingIRI   a mp:Recording ;
                    core:hasTitle ?titleIRI ;
                    core:hasYoutubeID ?youtubeID ;
                    mp:isRecordingProducedBy ?recordingProcessIRI;
                    mp:hasRecordingPerformer ?artistIRI .
    
    ...
```


Examples query to navigate through the knowlege graph are in the [query folder](test/queries):

You can also look at the graphoo images for the ontologies:

- [recordings and places](https://github.com/polifonia-project/sonar2021_demo/issues/14#issuecomment-917070412)
- [harmonic similarity](https://github.com/polifonia-project/sonar2021_demo/issues/21#issuecomment-946827230)



**Note:** ontologies and KGs are still in active development and may slightly be subject to changes. Due to this reason example queries or documentation can have some outdated parts. At the current state, the authoritative source for KG model are always [transformations](https://github.com/polifonia-project/KG_data_transformation#transformations) file listed at the link. You can always double check which files are harvested by [kg-harvester](kg-harvester/Dockerfile) and loaded in the SPARQL endpoint.


See also [this issue](https://github.com/polifonia-project/kg_sparql_endpoint/issues/1) linking to other queries for extracting data from the Polifonia KG, these ones will be added to the doc soon.

## Deploy

The following instructions show how to deploy the service.

#### Build the service

First of all download this codebase and cd to the downloaded folder:

`git clone https://github.com/polifonia-project/kg_sparql_endpoint.git && cd ./kg_sparql_endpoint`

Build command:

`docker-compose build`

#### Run the service

Launch the service (the `-d` flag will detach the process from current terminal):

`docker-compose up -d`

#### Stop the service

`docker-compose down`

#### Rebuild the service

Delete the volume with old triples and DB data:


`docker volume rm kg_sparql_endpoint_polifonia-kg`

Rebuild 


`docker-compose build --no-cache`

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
