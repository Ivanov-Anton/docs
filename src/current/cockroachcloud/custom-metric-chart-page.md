---
title: Custom Metric Chart Page
summary: The Custom Metric Chart page lets you create one or multiple custom charts showing the time series data for an available metric or combination of metrics.
toc: true
---

The **Custom Metric Chart** page is available for CockroachDB {{ site.data.products.serverless }} clusters. To view this page, select a cluster from the [**Clusters** page]({% link cockroachcloud/cluster-management.md %}#view-clusters-page), and click **Metrics** in the **Monitoring** section of the left side navigation. Navigate to the **Custom** tab to create one or multiple custom charts showing the time series data for an available metric or combination of metrics.

{{site.data.alerts.callout_info}}
{% include_cached feature-phases/preview.md %}
{{site.data.alerts.end}}

## Use the Custom Metric Chart page

<img src="{{ 'images/cockroachcloud/custom-metric-chart.png' | relative_url }}" alt="Custom Metric Chart" style="border:1px solid #eee;max-width:100%" />

On the **Custom Metric Chart** page, you can set the time range for all charts, add new custom charts, and customize each chart:

- To set the time range for the page, use the time interval selector at the top right of the page to filter the view for a predefined or custom time interval. Use the navigation buttons to move to the previous, next, or current time interval. When you select a time interval, the same interval is selected for all charts on all tabs of the [Metrics page]({% link cockroachcloud/metrics-page.md %}).
- To add a chart, click **Create** to create the first custom chart or **Add Chart** to create subsequent custom charts. The [**Create custom chart** modal](#create-custom-chart-modal) is displayed.
- To edit a chart, click the pencil icon to display the [**Edit custom chart** modal](#create-custom-chart-modal).
- To delete a chart, click the trash icon.

## Create custom chart modal

In the **Create custom chart** modal, you can customize each chart.

<img src="{{ 'images/cockroachcloud/custom-metric-chart-create.png' | relative_url }}" alt="Create Custom Chart" style="border:1px solid #eee;max-width:70%" />

- Under **Select metrics**, add the metrics to be queried, and how they'll be combined and displayed. Options include:
{% include cockroachcloud/ui-custom-metric-chart-page.html %}
- Under **Provide a chart name**, enter title text or keep default title with names of selected metrics.
- The **Preview** shows data, if available, for the selected metrics in the time range set by the Metrics page's time interval selector.
- Once the chart is verified in the **Preview**, click **Submit** to add the new custom chart or click **Close** to return to the existing **Custom Metric Chart** page.

## Available metrics for Serverless Deployments

{% include cockroachcloud/metric-names-serverless.md %}

## See also

- [Metrics Page]({% link cockroachcloud/metrics-page.md %})
