## Zipkin receiver
The Zipkin receiver makes the OAP server work as an alternative Zipkin server implementation for collecting traces. 
It supports Zipkin v1/v2 formats through the HTTP service.

Use the following config to activate it.
```yaml
receiver-zipkin:
  selector: ${SW_RECEIVER_ZIPKIN:default}
  default:
    # For HTTP server
    restHost: ${SW_RECEIVER_ZIPKIN_REST_HOST:0.0.0.0}
    restPort: ${SW_RECEIVER_ZIPKIN_REST_PORT:9411}
    restContextPath: ${SW_RECEIVER_ZIPKIN_REST_CONTEXT_PATH:/}
    restMaxThreads: ${SW_RECEIVER_ZIPKIN_REST_MAX_THREADS:200}
    restIdleTimeOut: ${SW_RECEIVER_ZIPKIN_REST_IDLE_TIMEOUT:30000}
    restAcceptQueueSize: ${SW_RECEIVER_ZIPKIN_REST_QUEUE_SIZE:0}
    searchableTracesTags: ${SW_ZIPKIN_SEARCHABLE_TAG_KEYS:http.method}
    # The sample rate precision is 1/10000, should be between 0 and 10000
    sampleRate: ${SW_ZIPKIN_SAMPLE_RATE:10000}
```

## Zipkin query
The Zipkin receiver makes the OAP server work as an alternative Zipkin server implementation for query traces. 
It implemented `ZipkinQueryApiV2` through the HTTP service, supporting Zipkin-lens UI.
**Notice: Zipkin query API implementation does not support BanyanDB yet.**

Use the following config to activate it.

```yaml
query-zipkin:
  selector: ${SW_QUERY_ZIPKIN:default}
  default:
    # For HTTP server
    restHost: ${SW_QUERY_ZIPKIN_REST_HOST:0.0.0.0}
    restPort: ${SW_QUERY_ZIPKIN_REST_PORT:9412}
    restContextPath: ${SW_QUERY_ZIPKIN_REST_CONTEXT_PATH:/zipkin}
    restMaxThreads: ${SW_QUERY_ZIPKIN_REST_MAX_THREADS:200}
    restIdleTimeOut: ${SW_QUERY_ZIPKIN_REST_IDLE_TIMEOUT:30000}
    restAcceptQueueSize: ${SW_QUERY_ZIPKIN_REST_QUEUE_SIZE:0}
    # Default look back for serviceNames, remoteServiceNames and spanNames, 1 day in millis
    lookback: ${SW_QUERY_ZIPKIN_LOOKBACK:86400000}
    # The Cache-Control max-age (seconds) for serviceNames, remoteServiceNames and spanNames
    namesMaxAge: ${SW_QUERY_ZIPKIN_NAMES_MAX_AGE:300}
    ## The below config are OAP support for zipkin-lens UI
    # Default traces query max size
    uiQueryLimit: ${SW_QUERY_ZIPKIN_UI_QUERY_LIMIT:10}
    # Default look back for search traces, 15 minutes in millis
    uiDefaultLookback: ${SW_QUERY_ZIPKIN_UI_DEFAULT_LOOKBACK:900000}
```
