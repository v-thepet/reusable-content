---
author: rboucher
ms.author: robb
ms.service: azure-monitor
ms.topic: include
ms.date: 01/17/2024
---

## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides key alert metrics, dashboards, and guidelines for Azure Landing Zone (ALZ) scenarios.

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

- [Metric alerts](/azure/azure-monitor/alerts/alerts-types#metric-alerts) evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.
- [Log alerts](/azure/azure-monitor/alerts/alerts-types#log-alerts) allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.
- [Activity log alerts](/azure/azure-monitor/alerts/alerts-types#activity-log-alerts) trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.
- [Smart detection alerts](/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts) on an Application Insights resource automatically warn you of potential performance problems and failure anomalies in your web application. You can migrate smart detection on your Application Insights resource to create alert rules for the different smart detection modules.
- [Prometheus alerts](/azure/azure-monitor/alerts/alerts-types#prometheus-alerts) alert on Prometheus metrics stored in [Azure Monitor managed services for Prometheus](/azure/azure-monitor/essentials/prometheus-metrics-overview.md). The alert rules are based on the PromQL open-source query language.

### Recommended alert rules

For some Azure services, you can [enable recommended out-of-the-box alert rules](/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

The system compiles a list of recommended alert rules based on:

- The resource provider's knowledge of important signals and thresholds for monitoring the resource.
- Data that tells what customers commonly alert on for this resource.

> [!NOTE]
> Recommended alert rules are available for:
> - Virtual machines
> - Azure Kubernetes Service (AKS) resources
> - Log Analytics workspaces

### Monitor multiple resources

You can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

