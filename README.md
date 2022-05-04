#This is a Prometheus exporter with Datadog

This is an example from the:
 - [open-telemetry repo](https://github.com/open-telemetry/opentelemetry-collector-contrib)

This code is found in the examples directory.

The docker-compose.yml file has been modified to add labels to the metrics container.
This allows Datadog auto-discover that the Datadog openmetrics check is required.

To run this example:

```shell
docker-compose up -d
```

Dockers starts 2 services:

- https://localhost:8088/metrics - Prometheus target that exports OpenTelemetry metrics.
- http://localhost:9090/graph - Prometheus configured to scrape our target.

For this exercise, the Prometheus scraper isn't required (although if you are curious you can play around)

Make sure you start the Dataog agent with the following options:

```
docker run -d --cgroupns host \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    -v /proc/:/host/proc/:ro \
    -v /sys/fs/cgroup/:/host/sys/fs/cgroup:ro \
    -e DD_API_KEY="<DATADOG_API_KEY>" \
    -e DD_SITE="<YOUR_DATADOG_SITE>" \
    gcr.io/datadoghq/agent:latest
```

**Note that you may need to attach the Datadog agent to the container created by docker-compose in order to use the %%host%%**

The counter presented will be:
```
test_my_counter
```

## See also

- [OpenTelemetry Metrics](https://opentelemetry.uptrace.dev/guide/metrics.html)
- [Datadog and Prometheus](https://docs.datadoghq.com/agent/docker/prometheus/?tab=dockercomposeyaml#simple-metric-collection)
