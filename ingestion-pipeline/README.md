# Ingestion Pipeline

This is the code used to ingest PubMed XMLs into ElasticSearch.

## Setup

We will first need to get ElasticSearch installed and running, after which we
can begin to upload content into the locally-running server.

### Start ElasticSearch

We recommend that you use docker to run ElasticSearch to avoid complications. Instructions
can be found [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html).


When your docker starts, you should see the following (it may take a couple minutes
to get started):
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Elasticsearch security features have been automatically configured!
✅ Authentication is enabled and cluster connections are encrypted.

ℹ️  Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  <password> 

ℹ️  HTTP CA certificate SHA-256 fingerprint:
  <very long hex string> 

ℹ️  Configure Kibana to use this cluster:
• Run Kibana and click the configuration link in the terminal when Kibana starts.
• Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  <very long token> 

ℹ️ Configure other nodes to join this cluster:
• Copy the following enrollment token and start new Elasticsearch nodes with `bin/elasticsearch --enrollment-token <token>` (valid for the next 30 minutes):
  <another very long token> 

  If you're running in Docker, copy the enrollment token and run:
  `docker run -e "ENROLLMENT_TOKEN=<token>" docker.elastic.co/elasticsearch/elasticsearch:8.6.2`
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
**Be sure to note** the password.

Also, **be sure to note** where you save the `http_ca.crt` file in the following command:
```bash
docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
```

### Fill ElasticSearch

Fill out the `config.ini` file in this directory, in particular updating the
password and the location of the certificate file.

You should then be able to simply run the pubmed processor:
```bash
python pubmed_processor.py --start -100 
```
The index will be created, and the content uploaded. You can check the options on the processor using `--help`.

Note that you will need to change the password, and update
the `http_ca.crt` file every time to start up ElasticSearch.