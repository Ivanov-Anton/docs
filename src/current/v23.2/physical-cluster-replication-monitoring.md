---
title: Physical Cluster Replication Monitoring
summary: Monitor and observe replication streams between a primary and standby cluster.
toc: true
docs_area: manage
---

{{site.data.alerts.callout_info}}
{% include feature-phases/preview.md %}
{{site.data.alerts.end}}

{% include_cached new-in.html version="v23.2" %}

You can monitor a replication stream in the following ways:

- Using `SHOW VIRTUAL CLUSTER ... WITH REPLICATION STATUS;`.
- On the DB Console {% comment %}add specific page{% endcomment %}.
- Using [Prometheus and Alertmanager](#prometheus) to track and alert on replication metrics.

{% comment %}Add data verification on standby here?{% endcomment %}


{% comment %}This page describes the available monitoring for physical cluster replication, for information on how replication works, refer to:{% endcomment %}

{% include {{ page.version.version }}/physical-replication/reference-links-replication.md %}

## SQL Shell

## DB Console

## Prometheus

{% comment %}metrics to validate (list below), improve descriptions, check on auto-pull in of metrics on metrics pages
Possible that a lot of these will not be relevant re multiple stream jobs happening at once...?
{% endcomment %}

`replication.events_ingested`: Events ingested by all replication jobs.
`replication.resolved_events_ingested`: Resolved events ingested by all replication jobs.
`replication.logical_bytes`: Logical bytes (sum of all keys + values) ingested by all replication jobs.
`replication.sst_bytes`: SST bytes (compressed) sent to KV by all replication jobs.
`replication.flushes`: Total flushes across all replication jobs.
`replication.flush_hist_nanos`: Time spent flushing messages across all replication streams.
`replication.commit_latency`: Event commit latency: a difference between the event MVCC timestamp and the time it was flushed into disk. If we batch events, the the difference between the oldest event in the batch and flish is recorded.
`replication.admit_latency`: Event admission latency: a difference between MVCC timestamp and the time it was admitted into the ingestion processor
`replication.running`: Number of currently running replication streams.
`replication.earliest_data_checkpoint_span`: The latest timestamp of the last checkpoint forwarded by an ingestion data processor.
`replication.data_checkpoint_span_count`: The number of resolved spans in the last checkpoint forwarded by an ingestion data processor.
`replication.frontier_checkpoint_span_count`: The number of resolved spans last persisted to the ingestion job's checkpoint record.
`replication.frontier_lag_nanos`: Time between the wall clock and replicated time of the replication stream. This metric tracks how far behind the replication stream is relative to now.
`replication.job_progress_updates`: Total number of updates to the ingestion job progress.
`replication.cutover_progress`: The number of ranges left to revert in order to complete an inflight cutover.
`replication.distsql_replan_count`: Total number of dist SQL replanning events.
