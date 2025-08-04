## Timeseries workload

timeseries.json contains the timeseries samples with the following structure, this workload is designed to benchmark
the OS's metrics engine.

### Example Document

```json
{
  "labels": [
    {
      "name": "__name__",
      "value": "http_requests_total"
    },
    {
      "name": "method",
      "value": "POST"
    },
    {
      "name": "handler",
      "value": "/api/items"
    },
    {
      "name": "status",
      "value": "200"
    }
  ],
  "samples": [
    {
      "value": 10.1,
      "timestamp": 1633072800000
    }
  ]
}
```

### Parameters

This workload allows [specifying the following parameters](#specifying-workload-parameters) using the `--workload-params` option to OpenSearch Benchmark:

* `bulk_size` (default: 10000)
* `ingest_percentage` (default: 100): A number between 0 and 100 that defines how much of the document corpus should be ingested.
* `number_of_replicas` (default: 0)
* `number_of_shards` (default: 1)
* `query_cache_enabled` (default: false)
* `requests_cache_enabled` (default: false)
* `source_enabled` (default: true): A boolean defining whether the `_source` field is stored in the index.
* `metrics_enabled` (default:true): A boolean flag indicating whether to turn on metrics engine.
* `wal_durability` (default:async): A flag to define the Write Ahead Log behavior.
* `wal_sync_interval` (default:1s): A variable defining the wal sync interval.
* `refresh_interval` (default:1s): A variable defining the index refresh interval.

### Specifying Workload Parameters

Example:
```json
{
  "trip_distance_mapping": { 
    "type": "unsigned_long" 
  } 
}
 ```

Save it as `params.json` and provide it to OpenSearch Benchmark with `--workload-params="/path/to/params.json"`. The overrides for simple parameters could be specified in-place, for example `--workload-params=search_clients:2`.

### Test Procedures
The workload contains multiple test procedures, see [TEST_PROCEDURES](TEST_PROCEDURES.md) for details.

