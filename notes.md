# Notes on gettinng up annd runninng
Start docker with the following commands
  1. ```docker run -v $HOME/git/annotation-data/images:/opt/solr/data/maars -p 8983:8983 dermotte/liresolr:latest```
  
The above command will start the default DOCKER container at docker hub, and mount your local `$HOME/git/annotation-data/images` directory to `/opt/solr/data/maars` on the container.

# Getting ready to index

Follow these instructions to begin indexing the MAARS data

## Generate the index_data.xml file and ingest the features

Run these commands:

  1. Print the image index: `find /opt/solr/data/maars -name "*.jpg" -print > /opt/solr/image_index.txt`
  2. Generate the XML ingest file using `ParallelIndexer`: 
      ```
      cd /opt/solr/server/solr-webapp/webapp/WEB-INF/lib && \
      java -cp ./lire.jar:./liresolr.jar net.semanticmetadata.lire.solr.indexing.ParallelSolrIndexer \
      -i /opt/solr/image_index.txt -o image_data.xml
      ```
  3. Ingest the XML file: 
     ```
     curl http://localhost:8983/solr/lire/update -H "Content-Type: text/xml" --data-binary @image_data.xml && \
     curl http://localhost:8983/solr/lire/update\?commit=true
     ```

## Run a query for similar images

This query will find all similar images to `/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_1.jpg` with accuracy of 1 (highest) and 100000 candidates (most):

```
http://localhost:8983/solr/lire/lireq?id=/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_1.jpg&accuracy=1&candidates=100000
```

This should return something like:

```
{
  "responseHeader":{
    "status":0,
    "QTime":66,
    "params":{
      "candidates":"100000",
      "accuracy":"1",
      "id":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_1.jpg"}},
  "QueryField":"cl_ha",
  "QueryFeature":"net.semanticmetadata.lire.imageanalysis.features.global.ColorLayout",
  "Note":"Switching to AllDocumentsQuery because accuracy is set higher than 0.9.",
  "DocValuesOpenTime":"0",
  "RawDocsCount":"10830",
  "RawDocsSearchTime":"12",
  "ReRankSearchTime":"47",
  "response":{"numFound":0,"start":0,"docs":[
      {
        "d":0.0,
        "title":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":3.1622776601683795,
        "title":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":3.1622776601683795,
        "title":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_2.jpg"},
      {
        "d":3.4641016151377544,
        "title":"/opt/solr/data/maars/ML0_407243459EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243459EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":3.605551275463989,
        "title":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":3.605551275463989,
        "title":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":3.7416573867739413,
        "title":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":3.7416573867739413,
        "title":"/opt/solr/data/maars/ML0_407243527EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243527EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":3.7416573867739413,
        "title":"/opt/solr/data/maars/ML0_493096917EDR_S0490814MCAM04734M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_493096917EDR_S0490814MCAM04734M1_2.jpg"},
      {
        "d":3.7416573867739413,
        "title":"/opt/solr/data/maars/ML0_493096964EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096964EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":3.872983346207417,
        "title":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_2.jpg"},
      {
        "d":4.0,
        "title":"/opt/solr/data/maars/ML0_460516848EDR_S0400366MCAM03016M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_460516848EDR_S0400366MCAM03016M1_2.jpg"},
      {
        "d":4.0,
        "title":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_1.jpg"},
      {
        "d":4.123105625617661,
        "title":"/opt/solr/data/maars/ML0_407243527EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243527EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":4.242640687119285,
        "title":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_4.jpg",
        "id":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_4.jpg"},
      {
        "d":4.242640687119285,
        "title":"/opt/solr/data/maars/ML0_493468608EDR_S0491216MCAM04757M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493468608EDR_S0491216MCAM04757M1_0.jpg"},
      {
        "d":4.242640687119285,
        "title":"/opt/solr/data/maars/ML0_493468624EDR_S0491216MCAM04757M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493468624EDR_S0491216MCAM04757M1_0.jpg"},
      {
        "d":4.358898943540674,
        "title":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_407243617EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243617EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_460516447EDR_S0400366MCAM03015M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_460516447EDR_S0400366MCAM03015M1_0.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_460879698EDR_S0400762MCAM03039M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_460879698EDR_S0400762MCAM03039M1_1.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_463717373EDR_S0411570MCAM03208M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_463717373EDR_S0411570MCAM03208M1_1.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_464174849EDR_S0420852MCAM03229M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_464174849EDR_S0420852MCAM03229M1_0.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_2.jpg"},
      {
        "d":4.47213595499958,
        "title":"/opt/solr/data/maars/ML0_493096917EDR_S0490814MCAM04734M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_493096917EDR_S0490814MCAM04734M1_1.jpg"},
      {
        "d":4.58257569495584,
        "title":"/opt/solr/data/maars/ML0_407243639EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243639EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":4.58257569495584,
        "title":"/opt/solr/data/maars/ML0_493096842EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096842EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":4.58257569495584,
        "title":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_3.jpg"},
      {
        "d":4.58257569495584,
        "title":"/opt/solr/data/maars/ML0_493558295EDR_S0491216MCAM04761M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_493558295EDR_S0491216MCAM04761M1_2.jpg"},
      {
        "d":4.69041575982343,
        "title":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_407243437EDR_S0050388AUT_04096M1_3.jpg"},
      {
        "d":4.69041575982343,
        "title":"/opt/solr/data/maars/ML0_407243459EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243459EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":4.69041575982343,
        "title":"/opt/solr/data/maars/ML0_460879698EDR_S0400762MCAM03039M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_460879698EDR_S0400762MCAM03039M1_0.jpg"},
      {
        "d":4.795831523312719,
        "title":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_2.jpg"},
      {
        "d":4.795831523312719,
        "title":"/opt/solr/data/maars/ML0_407243571EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243571EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":4.795831523312719,
        "title":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_1.jpg"},
      {
        "d":4.795831523312719,
        "title":"/opt/solr/data/maars/ML0_493096870EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096870EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243481EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_407243549EDR_S0050388AUT_04096M1_2.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_464174849EDR_S0420852MCAM03229M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_464174849EDR_S0420852MCAM03229M1_1.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_464255470EDR_S0420852MCAM03232M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_464255470EDR_S0420852MCAM03232M1_0.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_493096842EDR_S0490814MCAM04734M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_493096842EDR_S0490814MCAM04734M1_1.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_494260007EDR_S0491876MCAM04786M1_4.jpg",
        "id":"/opt/solr/data/maars/ML0_494260007EDR_S0491876MCAM04786M1_4.jpg"},
      {
        "d":4.898979485566356,
        "title":"/opt/solr/data/maars/ML0_494260007EDR_S0491876MCAM04786M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_494260007EDR_S0491876MCAM04786M1_3.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_407243394EDR_S0050388AUT_04096M1_3.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_407243571EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243571EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_460516814EDR_S0400366MCAM03016M1_4.jpg",
        "id":"/opt/solr/data/maars/ML0_460516814EDR_S0400366MCAM03016M1_4.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_460516848EDR_S0400366MCAM03016M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_460516848EDR_S0400366MCAM03016M1_1.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096824EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":5.0,
        "title":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_493096935EDR_S0490814MCAM04734M1_2.jpg"},
      {
        "d":5.0990195135927845,
        "title":"/opt/solr/data/maars/ML0_407243617EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243617EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":5.0990195135927845,
        "title":"/opt/solr/data/maars/ML0_407243686EDR_S0050388AUT_04096M1_1.jpg",
        "id":"/opt/solr/data/maars/ML0_407243686EDR_S0050388AUT_04096M1_1.jpg"},
      {
        "d":5.0990195135927845,
        "title":"/opt/solr/data/maars/ML0_407243732EDR_S0050388AUT_04096M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_407243732EDR_S0050388AUT_04096M1_0.jpg"},
      {
        "d":5.0990195135927845,
        "title":"/opt/solr/data/maars/ML0_460516640EDR_S0400366MCAM03015M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_460516640EDR_S0400366MCAM03015M1_2.jpg"},
      {
        "d":5.0990195135927845,
        "title":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_0.jpg",
        "id":"/opt/solr/data/maars/ML0_493096888EDR_S0490814MCAM04734M1_0.jpg"},
      {
        "d":5.196152422706632,
        "title":"/opt/solr/data/maars/ML0_407332765EDR_S0050388AUT_04096M1_2.jpg",
        "id":"/opt/solr/data/maars/ML0_407332765EDR_S0050388AUT_04096M1_2.jpg"},
      {
        "d":5.196152422706632,
        "title":"/opt/solr/data/maars/ML0_407332765EDR_S0050388AUT_04096M2_3.jpg",
        "id":"/opt/solr/data/maars/ML0_407332765EDR_S0050388AUT_04096M2_3.jpg"},
      {
        "d":5.196152422706632,
        "title":"/opt/solr/data/maars/ML0_460516640EDR_S0400366MCAM03015M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_460516640EDR_S0400366MCAM03015M1_3.jpg"},
      {
        "d":5.196152422706632,
        "title":"/opt/solr/data/maars/ML0_460516814EDR_S0400366MCAM03016M1_3.jpg",
        "id":"/opt/solr/data/maars/ML0_460516814EDR_S0400366MCAM03016M1_3.jpg"}]
  }}

```
 
