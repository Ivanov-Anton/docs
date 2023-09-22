---
title: Cut Over from a Primary Cluster to a Standby Cluster
summary: A guide complete physical cluster replication and cut over from a primary to a standby cluster.
toc: true
docs_area: manage
---

{{site.data.alerts.callout_info}}
{% include feature-phases/preview.md %}
{{site.data.alerts.end}}

{% include_cached new-in.html version="v23.2" %} Physical cluster replication allows you to cut over from an active primary cluster to the passive standby cluster that has ingested replicated data. When you complete the replication, it will stop the stream of new data, reset the standby virtual cluster to a point in time where all ingested data is consistent, and then mark the standby virtual cluster as ready to accept traffic.

You can initiate a cutover to the standby cluster in a couple of different ways. Refer to the following sections for steps:

- [`LATEST`](#cut-over-to-the-most-recent-replicated-time): The most recent timestamp that the standby virtual cluster can be consistent.
- [Point-in-time](#cut-over-to-a-point-in-time):
    - Past: A timestamp in the past that is within the cutover window. {% comment %}Add link to technical overview{% endcomment %}
    - Future: A timestamp in the future that plans a cutover.

{{site.data.alerts.callout_info}}
Initiating a cutover is a manual process that makes the standby cluster ready to accept SQL connections. From this point, you will need to ensure that a load balancer {% comment %}or other infra{% endcomment %} redirects application traffic to the standby cluster.
{{site.data.alerts.end}}

{% comment %}This page describes how to cut over from the primary to the standby cluster, for information on how replication works, refer to:{% endcomment %}

{% include {{ page.version.version }}/physical-replication/reference-links-replication.md %}

## Cut over to the most recent replicated time

To cut over to the most recent replicated timestamp that will leave the standby virtual cluster in a transactionally consistent state, use `LATEST`:

{% include_cached copy-clipboard.html %}
~~~ sql
ALTER VIRTUAL CLUSTER application COMPLETE REPLICATION TO LATEST;
~~~

The completion of the replication is asynchronous; to monitor its progress use:

{% include_cached copy-clipboard.html %}
~~~ sql
SHOW VIRTUAL CLUSTER application WITH REPLICATION STATUS;
~~~

Once the `replication_status`

{% include_cached copy-clipboard.html %}
~~~ sql
ALTER VIRTUAL CLUSTER application START SERVICE SHARED;
~~~

## Cut over to a point in time

You can control the point in time that the replication stream will cut over to.

To select a [specific time]({% link {{ page.version.version }}/as-of-system-time.md %}) in the past, use:

{% include_cached copy-clipboard.html %}
~~~ sql
SHOW VIRTUAL CLUSTER application WITH REPLICATION STATUS;
~~~

The `retained_time` response provides the earliest time to which you can cut over.

Specify a timestamp:

{% include_cached copy-clipboard.html %}
~~~ sql
ALTER VIRTUAL CLUSTER application COMPLETE REPLICATION TO SYSTEM TIME '-1h';
~~~

Refer to [Using different timestamp formats]({% link {{ page.version.version }}/as-of-system-time.md %}#using-different-timestamp-formats) for more information.

Similarly, to cut over to a specific time in the future:

{% include_cached copy-clipboard.html %}
~~~ sql
ALTER VIRTUAL CLUSTER application COMPLETE REPLICATION TO SYSTEM TIME '+5h';
~~~

A future cutover will proceed once the replicated data has reached the specified time.

## Completing cutover

At this point, the primary and standby clusters are entirely independent.

You will need to use your own orchestration to direct traffic to the standby. Perhaps this is done by updating a load balancer, DNS, or connection string.

{% comment %}complete section{% endcomment %}
