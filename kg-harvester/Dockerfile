FROM alpine:3.14

RUN apk add wget

# cd in the volume dir where virtuoso endpoint search for triples
# see: [pointer to virtuoso dock]
WORKDIR /data/toLoad



### Downloading KG triples
# places
RUN wget https://raw.githubusercontent.com/polifonia-project/KG_data_transformation/master/polifonia_places_etl/kg/polifonia-kg-places-latest.ttl
# harmonic similarity
RUN wget https://raw.githubusercontent.com/polifonia-project/KG_data_transformation/master/harmonic_sim_etl/kg/polifonia-kg-harmonic-sim-latest.ttl


### Downloading ontologies
# cm
RUN wget https://raw.githubusercontent.com/polifonia-project/comparative-measure/main/comparative-measure.owl

# harmonic sym
RUN wget https://raw.githubusercontent.com/polifonia-project/comparative-measure/main/harmonic-similarity.owl

# core
RUN wget https://raw.githubusercontent.com/polifonia-project/core/main/core.owl

# core aligns
RUN wget https://raw.githubusercontent.com/polifonia-project/core/main/core-aligns.owl

# musical performance
RUN wget https://raw.githubusercontent.com/polifonia-project/musical-performance/main/musical-performance.owl

# musical composition
RUN wget https://raw.githubusercontent.com/polifonia-project/musical-composition/main/musical-composition.owl
