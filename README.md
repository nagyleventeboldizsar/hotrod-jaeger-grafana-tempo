# HotROD implementation with Grafana - Grafana Tempo - Grafana Loki - OTEL Collector

Highly inspired by [jaeger example HOT ROD demo app](https://github.com/jaegertracing/jaeger/tree/main/examples/hotrod)

This example combines the Hot R.O.D. demo application  with Grafana, Loki and Prometheus integration, to demonstrate logs, metrics and traces correlation. Implementation of tracing consists of jaeger-agent, otel-collector and grafana tempo.

## Running via `docker-compose`

### Prerequisites

* Clone the given repository

* install [Loki Logging driver for Docker ](https://grafana.com/docs/loki/latest/clients/docker-driver/)

### Run the services

`docker-compose up -d ` 

### Access the services
* HotROD application at http://localhost:8080
* Grafana UI at http://localhost:3000

### Explore with Loki

It is possible to correlate application logs with traces via Grafana's Explore interface.

After setting the datasource to Loki, all the log labels become available, and can be easily filtered using [Loki's LogQL query language](https://grafana.com/docs/loki/latest/logql/).

For example, after selecting the compose project/service under Log labels , errors can be filtered with the following expression:

```
{compose_project="grafana-integration"} |= "error"
```

which will list the redis timeout events.

### HotROD - Metrics and logs overview dashboard

Since the HotROD application can expose its metrics in Prometheus' format, these can be also used during investigation.

This example includes a dashboard that contains a log panel for the selected services in real time. These can be also filtered by a search field, that provides `grep`-like features.

There are also panels to display the ratio/percentage of errors in the current timeframe.

Additionally, there are graphs for each service, visualizing the rate of the requests and showing latency percentiles.

### Clean up

`docker-compose down`
