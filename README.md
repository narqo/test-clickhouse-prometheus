# test-clickhouse-prometheus

Test Prometheus remote-write/-read interface in ClickHouse.

This ClickHouse support relies on the experimental [`TimeSeries` engine][1]. Refer to the [docs][1] for details.

## Run

```
% docker compose up
```

Execute a test query through Prometheus (the UI is runnin on `http://127.0.0.1:9090`)

```
% curl -v 'http://127.0.0.1:9090/api/v1/query?query=sum(ClickHouseAsyncMetrics_DiskUsed_default)'
```

### Inspect the data with clickhouse-client

```
% docker container run --rm -ti --network test-clickhouse-prometheus_default --entrypoint=clickhouse clickhouse/clickhouse-server:head client -h clickhouse-server

d72188fcebe0 :) show tables
...
```

[1]: https://clickhouse.com/docs/en/engines/table-engines/special/time_series
[2]: https://clickhouse.com/docs/en/interfaces/prometheus
