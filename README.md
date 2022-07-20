# Telemetry stacks
This setup uses Loki for logs, Prometheus for metrics, and Jaeger for tracing. It will automatically collect logs from other Docker containers running on the same server if the installation steps below are followed.

The stack includes the following:

* **cAdvisor** [[Docs](https://github.com/google/cadvisor)] [[Local UI](http://localhost:9081/)] - Provides resource usage and performance metrics of Docker containers to Prometheus
* **Grafana** [[Docs](https://grafana.com/docs/grafana/latest/)] [[Local UI](http://localhost:3000/)] - UI to explore logs and metrics using queries, charts, and alerts
* **Jaeger** [[Docs](https://www.jaegertracing.io/docs/)] [[Local UI](http://localhost:16686/)] - Provides tracing data which is linked to each incoming server request
* **Loki** [[Docs](https://grafana.com/docs/loki/latest/)] - Ingests logs which can be viewed and queried from within Grafana
* **OpenTelemetry Collector** [[Docs](https://opentelemetry.io/docs/collector/)] - Collects metrics data from server and exports the data to Prometheus
* **Zipkin** [[Docs] (https://zipkin.io/pages/quickstart)] - A distributed tracing system, it helps gather timing data needed to troubleshoot latency problems in service architectures
* **Prometheus** [[Docs](https://prometheus.io/docs/)] [[Local UI](http://localhost:3001/)] - A monitoring toolkit for timeseries based metrics
* **Vector** [[Docs](https://vector.dev/docs/)] - Transforms Docker logs and send them to Loki, as well as collecting logs from local Node.js processes if required

## Installation

- Clone the repository and launch cAdvisor, Grafana, Jaeger, Loki, OpenTelemetry Collector, Prometheus, and Vector:
  ```sh
  git clone git@github.com:cybergitt/telemetry-stacks.git
  cd telemetry-stacks
  docker-compose up -d
  ```
- Navigate to <http://localhost:3000/> and log in using the default Grafana user (admin/admin).

## Troubleshooting

### Jaeger EMSGSIZE error

Jaeger needs higher UDP package sizes than the maximum configured on Mac. The default value should be increased using:
```sh
sudo sysctl net.inet.udp.maxdgram=65536
```