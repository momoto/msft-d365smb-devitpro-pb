---
title: "Operation Limits in Dynamics 365 Business Central"
description: ""
author: jswymer
ms.custom: na
ms.date: 04/01/2020
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: "dynamics-nav-2018"
ms.author: jswymer
---

# Operational Limits for Business Central Online

To ensure the availability and quality of Business Central services, there are limits on certain operations. This article describes the limits and, in some cases, the strategy behind them.

> [!TIP]
> Telemetry is gathered on some of the operations that have a limit. The telemetry provides insight into operations for which limits were exceeded. For more information, see [Monitoring and Analyzing Telemetry](telemetry-overview.md).

<!--
For [!INCLUDE[prodshort](../developer/includes/prodshort.md)] online, you can't change these limits, but it's useful to be aware of them. For on-premises installation, you can adjust most of the limits by configuring the [!INCLUDE[server](../developer/includes/server.md)].-->

##  <a name="ClientServices"></a> Client connection limits
  
|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
|Max concurrent calls|The maximum number of concurrent client calls that can be active.|1000|  
|Max concurrent connections|The maximum number of concurrent client connections that the service accepts. |500|
|Max number of orphaned connections|Th maximum number of orphaned connections to be kept alive at the same time for the time that is specified by **ReconnectPeriod**.<br /><br /> A connection is orphaned when the client is involuntarily disconnected from service.<br /><br /> You can also use **MaxValue** as a value to indicate no limit.o| 20|
|Reconnect period|The time during which a client can reconnect to the service after being disconnected.|  10 minutes|

<!-- no limit
|Operation timeout|The maximum time for the service to return a call from the client.||  
-->
##  <a name="ClientServices"></a> Data handling limits
  
|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
|Max items in object graph|The maximum number of objects to serialize or deserialize.|  10,000|
|Max file size|The maximum size of files that can be uploaded to or downloaded from the service.|350 MB|
|Maximum stream read size|The maximum number of bytes that can be read from a stream (InStream object) in a single AL read operation. Examples include READ or InStream.READTEXT method calls. This setting pertains to UTF-8 and UTF-16 text encoding; not MS-DOS encoding. |1,000,000 bytes|

<!--
|Max data rows allowed to send to excel|The maximum number of rows that can be included in an Excel document generated from a list type page <br /><br /> **Note:** This setting only pertains to list type pages in the client. For other pages types, the limit on rows is configured in the client.| |    
|Data cache size|The contextual size of the data cache.| 9| 
|Chunk size|The default size for a chunk of data that is transferred between the service and clients| 28 KB| 
|Compression threshold|The threshold in memory consumption at which the service starts compressing datasets| 64 KB|
-->

##  <a name="Database"></a> Database connection limits
  
|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Value|  
|---------|--------------------------------------------------------------------------------|------|
|Search timeout|The time (in seconds) that a search operation on lists in the client continues before it's stopped. When the limit is reached, the following message displays in the client: **Searching for rows is taking too long. Try to search or filter using different criteria.**|10 seconds|
|SQL command timeout|The contextual time-out for a SQL command.|30 minutes|
|SQL connection idle timeout|The time that a SQL connection can remain idle before being closed.|5 minutes|
|SQL connection timeout|The time to wait for the service to connect to the database. When the time is exceeded, the attempt is canceled and an error occurs. This setting also applies to begin, rollback, and commit of transactions.|1.5 hours|
|Long running SQL query threshold|The amount of time that an SQL query can run before a warning telemetry event occurs. If this threshold is exceeded, the following event is logged: Action completed successfully, but it took longer than the given threshold.|1000 ms|

<!--
|SQL bulk import batch size|Specifies how many SQL memory chunks that a data import must be distributed across.| 448|
-->
## <a name="Task"></a>Asynchronous task limits

|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
|  Maximum concurrent running scheduled tasks  | The maximum number of tasks that can run simultaneously on the server instance.<br /><br />If there are many jobs running at the same time, you might experience that the response time for clients gets slower. If the value is too low, it might take longer for scheduled tasks to process.|10|
|  Page background task default timeout |The default amount of time that page background tasks can run before being canceled. Page background tasks can be also given a timeout value when enqueued at runtime. This limit is used when no timeout is provided when the page background task is enqueued.|2 minutes|
|  Page background task max timeout | The maximum amount of time that page background tasks can run before being canceled. Page background tasks can be also given a timeout value when enqueued at runtime. If a page background task is enqueued with a timeout greater than this limit, this limit is ignored.|10 minutes|
|ChildSessionsMaxConcurrency|The maximum number of child sessions that can run concurrently per parent session. When the value is exceeded, additional child sessions will be queued and run when a slot becomes available as other child sessions are finished.|5|
|ChildSessionsMaxQueueLength|The maximum number of child sessions that can be queued per parent session. If the value is exceeded, an error occurs.|100|

## Report limits

|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
| Max execution timeout | The maximum execution time that it can take to generate a report. If exceeded, the report will be canceled.|12 hours|
| Max rows | The maximum number of rows that can be processed in a report. If exceeded, the report will be canceled by the server.|1,000,000|
|Max execution timeout for Word reports| The maximum execution time that it can take to generate a report that uses a Word layout. If exceeded, the report will be canceled.|30 minutes|

## Query limits

|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
| Max execution timeout | The maximum execution time that it can take to generate a query. If exceeded, the query will be canceled.|30 minutes|
| Max rows | The maximum number of rows that can be processed in a query. If exceeded, the query will be canceled.|1,000,000|

##  <a name="ODataServices"></a> OData request limits
  
|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
|Max connections|The maximum number of simultaneous OData requests on the server instance. When the limit is exceeded, a 429 (Too Many Requests) error occurs.|100 |
|Max page size|The maximum number of entities returned per page of OData results.|  20,000 entities per page|
|Rate|The number of OData requests per minute that are allowed. An HTTP response code `429 - Too Many Requests` is returned if limits are exceeded.|Sandbox:<br />300 requests/minute<br /><br />Production<br />- 600 requests/minute| 
|Operation timeout|The maximum amount of time that the service gives a single SOAP request. When the limit is exceeded, an HTTP response code `408 - Request Timeout` is returned.|10 minutes|

<!--
|Request timeout|HTTP response code `504 - Gateway Timeout` is returned when a request exceeds 10-minutes execution time.|10 minutes|
-->
##  <a name="SOAPServices"></a> SOAP request limits

|Setting|[!INCLUDE[bp_tabledescription](../developer/includes/bp_tabledescription_md.md)]| Limit|  
|---------|--------------------------------------------------------------------------------|------|
|Maximum connections|The maximum number of simultaneous SOAP requests on the server instance. When the limit is exceeded, a `429 (Too Many Requests)` error occurs.|100 |
|Maximum message size|The maximum permitted size of a SOAP web service requests|65,536 KB|
|Rate|Specifies how many SOAP requests per minute are allowed. An HTTP response code `429 - Too Many Requests` is returned if limits are exceeded.|Sandbox:<br /> 300 requests/minute<br /><br />Production:<br />600 requests/minute|
|Operation timeout|The maximum amount of time that the service gives to a single SOAP request. When the limit is exceeded, HTTP response code `408 - Request Timeout` is returned.|8 minutes|

<!--
|Request timeout|HTTP response code `504 - Gateway Timeout` is returned when a request exceeds 10-minutes execution time.|10 minutes|
-->
## See Also

[Working with API Rate Limits](/dynamics-nav/api-reference/v1.0/dynamics-rate-limits)  
[Microsoft API Terms of Use](https://docs.microsoft.com/legal/microsoft-apis/terms-of-use)  