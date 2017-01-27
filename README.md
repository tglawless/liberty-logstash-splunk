# Sending WebSphere Liberty Logs to Splunk

## Overview
This repository contains an example configuration for sending the log entries from a containerized WebSphere Liberty profile server to Splunk.  The example utilizes the Liberty Profile Logstach Collector feature and a containerized Logstash server to stream log entriess from the Liberty container to Logstash.  Logstash is used to format the log entry and send it to Splunk's HTTP event collector.

## Running the example

The container stack requires 2 environment varaible to be set.  From a terminal window, execute the following:

```
# The value of this variable should be in the form of
# input-<UNIQUE HOSTNAME>.cloud.splunk.com
export SPLUNK_HOST=<YOUR SPLUNK CLOUD HOSTNAME>

# This value should be the token created by Splunk when
# a new HTTP Event Collector is created.
export SPLUNK_TOKEN=<YOUR SPLUNK CLOUD HTTP EVENT COLLECTOR TOKEN>
```

In the same terminal window, start the container stack using:

```
docker-compose up
```

Within a few seconds of the containers starting up, the log entries from the Liberty server will be visible in Splunk for search and custom dashboards.

***NOTE: Remember to generate your own SSL certificates for Logstash if you are going to reuse this example for something real.***

## Alternatives

Once the log entries are streamed into Logstash, Splunk is just one option for their final destination.  They could easily be sent to Elasticsearch if you are running an ELK stack or other SaaS solutions like New Relic, Datadog or Loggly just to name a few. 



