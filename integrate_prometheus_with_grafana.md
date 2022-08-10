# Prometheus and Grafana

## Installation using docker
Prometheus:- `docker run -p 9090:9090 prom/prometheus`
Grafana:-`docker run -d -p 3000:3000 grafana/grafana-enterprise`

## Start server
Prometheus:- http://localhost:9090
Grafana:- http://localhost:3000

Note: If you have Docker Compose seperately installed, `localhost` or `127.0.0.1` probably won't work, instead use your machine's ip address.

## Understanding metrics
Metrics are numeric measurements

## Instrumenting code
In order for Prometheus to scrape metrics from a service, the service must satisfy the format and structure needed to export the metrics to prometheus.

## Exporters

Exporters are binaries that acts as a middleware which converts the metrics exposed by any 3rd party application/software into a format that prometheus can understand and scrape through their metrics. Examples: NodeExporter, cAdvisor
We can develop personalised exporters for our applications by following the guidelines and best practices documented... 


## Integrating metrics

### blackbox metrics exporter
```
- job_name: 'blackbox'
    metrics_path: /metrics
    params:
      module: [http_2xx]  # Look for a HTTP 200 response.
    static_configs:
      - targets: # Target to probe with https.
        - http://*your_ip_address*:9115 # Target to probe with http on port 8080.
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: *your_ip_address*:9115  # The blackbox exporter's real hostname:port.
```
        
if config setup is succesful then all the metrics blackbox exporter has to offer will be hosted on http://localhost:9115
![](https://i.imgur.com/4YMQhgO.jpg)



These are the metrics that are exported through blackbox to prometheus
![](https://i.imgur.com/BZbXGKw.png)


## Connecting Grafana with Prometheus

Configure the data-source of prometheus with the grafana service so that grafana can query the data from the local prometheus server.

Steps
Create new data source
under http url enter http://*your_ip_address*:9115
Save


## Creating Dashboard to visualise metrics


