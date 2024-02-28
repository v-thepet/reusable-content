---
author: rboucher
ms.author: robb
ms.service: azure-monitor
ms.topic: include
ms.date: 02/27/2024
---

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.
- You can optionally route metric and activity log data to the Azure Monitor logs database store so you can query the data and correlate it with other log data using Log Analytics.

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/azure/azure-monitor/platform/data-platform).
