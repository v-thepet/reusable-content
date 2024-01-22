---
author: rboucher
ms.author: robb
ms.service: azure-monitor
ms.topic: include
ms.date: 01/17/2024
---

## Platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route platform metrics to Azure Monitor logs so you can query them with other log data. For more information, see [Azure Monitor Agent overview](/azure/azure-monitor/agents/agents-overview).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/azure/azure-monitor/platform/metrics-supported).
