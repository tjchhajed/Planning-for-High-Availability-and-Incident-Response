## Availability SLI
### The percentage of successful requests over the last 5m
sum(rate(flask_http_request_total{status=~"201"} [5m]))/sum(rate(flask_http_request_total [5m]))

## Latency SLI
### 90% of requests finish in these times
histogram_quantile(0.90, sum(rate(flask_http_request_duration_seconds_bucket [5m]))  by (le, verb))

## Throughput
### Successful requests per second
sum(rate(flask_http_request_total{status=~"201"} [5m]))

## Error Budget - Remaining Error Budget
### The error budget is 20%
1 - ((1-sum(increase(flask_http_request_total{status=~"201"}[1d]))  by (verb)) / (sum(increase(flask_http_request_total[1d]))  by (verb)) / (1 - .90))
or 
1 - ((1-(flask_http_request_total{status=~"201"})  by (verb)) / flask_http_request_total by (verb)) / (1 - .90))
