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
* `bulk_indexing_clients` (default: 8): Number of clients that issue bulk indexing requests.
* `ingest_percentage` (default: 100): A number between 0 and 100 that defines how much of the document corpus should be ingested.
* `conflicts` (default: "random"): Type of id conflicts to simulate. Valid values are: 'sequential' (A document id is replaced with a document id with a sequentially increasing id), 'random' (A document id is replaced with a document id with a random other id).
* `conflict_probability` (default: 25): A number between 0 and 100 that defines the probability of id conflicts. Only used by the `update` test_procedure. Combining ``conflicts=sequential`` and ``conflict-probability=0`` makes Benchmark generate index ids by itself, instead of relying on OpenSearch's `automatic id generation`.
* `on_conflict` (default: "index"): Whether to use an "index" or an "update" action when simulating an id conflict. Only used by the `update` test_procedure.
* `recency` (default: 0): A number between 0 and 1 that defines whether to bias towards more recent ids when simulating conflicts. See the [Benchmark docs](https://github.com/opensearch-project/OpenSearch-Benchmark/blob/main/DEVELOPER_GUIDE.md) for the full definition of this parameter. Only used by the `update` test_procedure.
* `number_of_replicas` (default: 0)
* `number_of_shards` (default: 1)
* `query_cache_enabled` (default: false)
* `requests_cache_enabled` (default: false)
* `source_enabled` (default: true): A boolean defining whether the `_source` field is stored in the index.
* `force_merge_max_num_segments` (default: unset): An integer specifying the max amount of segments the force-merge operation should use.
* `index_settings`: A list of index settings. Index settings defined elsewhere (e.g. `number_of_replicas`) need to be overridden explicitly.
* `cluster_health` (default: "green"): The minimum required cluster health.
* `error_level` (default: "non-fatal"): Available for bulk operations only to specify ignore-response-error-level.
* `target_throughput` (default: default values for each operation): Number of requests per second, `none` for no limit.
* `search_clients`: Number of clients that issues search requests.
* `trip_distance_mapping` (default: { "scaling_factor": 100, "type": "scaled_float" }): The `trip_distance` field type mapping

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

