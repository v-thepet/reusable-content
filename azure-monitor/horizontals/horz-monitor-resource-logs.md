---
author: rboucher
ms.author: robb
ms.service: azure-monitor
ms.topic: include
ms.date: 01/17/2024
---

## Resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized by category. A given namespace might have multiple resource log categories you can collect.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy. For more information, see [Diagnostic setting destinations](/azure/azure-monitor/essentials/diagnostic-settings#destinations).

**Routing:** The suggested default is to route resource logs to Azure Monitor logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/azure/azure-monitor/essentials/resource-logs).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/azure/azure-monitor/essentials/resource-logs-schema).

>>>>TODO - possible inclusion of a screenshot showing how to enable these in portal 
