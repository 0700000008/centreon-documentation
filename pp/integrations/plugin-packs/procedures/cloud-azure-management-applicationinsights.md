---
id: cloud-azure-management-applicationinsights
title: Azure Application Insights
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Overview

Azure Applications Insights extends the functionality of Azure Monitor to
observe applications in real time.

The Centreon Monitoring Connector *Azure Application Insights* can rely on Azure API or Azure CLI to collect the metrics related to the
Application Gateway service.

## Pack Assets

### Monitored Objects

* Azure *Application Insights* instances
    * Availability   
    * Browser-Timings
    * Cpu
    * Exceptions
    * External-Calls   
    * IO-Operations  
    * Memory 
    * Requests          

### Discovery rules

The Centreon Monitoring Connector *Azure Application Insights* includes a Host Discovery *provider* to automatically discover the Azure instances of a given
subscription and add them to the Centreon configuration.
This provider is named **Microsoft Azure Application Insights**:

![image](../../../assets/integrations/plugin-packs/procedures/cloud-azure-management-applicationinsights-provider.png)

> This discovery feature is only compatible with the 'api' custom mode. 'azcli' is not supported yet.

More information about the Host Discovery module is available in the Centreon documentation:
[Host Discovery](/docs/monitoring/discovery/hosts-discovery)

### Collected metrics & status

<Tabs groupId="sync">
<TabItem value="Availability" label="Availability">

| Metric Name                                          | Description                | Unit  |
|:-----------------------------------------------------|:---------------------------|:------|
| appinsights.availability.percentage                  | Availability               | %     |
| appinsights.availability.tests.count                 | Availability tests         | Count |
| appinsights.availability.tests.duration.milliseconds | Availability test duration | ms    |

</TabItem>
<TabItem value="Browsertimings" label="Browsertimings">

| Metric Name                                  | Description                    | Unit |
|:---------------------------------------------|:-------------------------------|:-----|
| appinsights.processing.duration.milliseconds | Client processing time         | ms   |
| appinsights.processing.duration.milliseconds | Page load network connect time | ms   |
| appinsights.receive.duration.milliseconds    | Receiving response time        | ms   |
| appinsights.send.duration.milliseconds       | Send request time              | ms   |
| appinsights.total.duration.milliseconds      | Browser page load time         | ms   |

</TabItem>
<TabItem value="Cpu" label="Cpu">

| Metric Name                                 | Description    | Unit |
|:--------------------------------------------|:---------------|:-----|
| appinsights.cpu.nonidle.time.percentage     | Processor time | %    |
| appinsights.cpu.w3wp.utilization.percentage | Process CPU    | %    |

</TabItem>
<TabItem value="Exceptions" label="Exceptions">

| Metric Name                          | Description        | Unit  |
|:-------------------------------------|:-------------------|:------|
| appinsights.exceptions.browser.count | Browser exceptions | Count |
| appinsights.exceptions.server.count  | Server exceptions  | Count |
| appinsights.exceptions.total.count   | Exceptions         | Count |

</TabItem>
<TabItem value="Externalcalls" label="Externalcalls">

| Metric Name                             | Description              | Unit  |
|:----------------------------------------|:-------------------------|:------|
| appinsights.calls.count                 | Dependency calls         | Count |
| appinsights.calls.duration.milliseconds | Dependency duration      | ms    |
| appinsights.calls.failure.count         | Dependency call failures | Count |

</TabItem>
<TabItem value="Iooperations" label="Iooperations">

| Metric Name                                        | Description     | Unit |
|:---------------------------------------------------|:----------------|:-----|
| appinsights.process.bytes.operations.bytesperseconds | Process IO rate | B/s  |

</TabItem>
<TabItem value="Memory" label="Memory">

| Metric Name                        | Description           | Unit |
|:-----------------------------------|:----------------------|:-----|
| appinsights.memory.available.bytes | Available memory      | B    |
| appinsights.memory.private.bytes   | Process private bytes | B    |

</TabItem>
<TabItem value="Pageviews" label="Pageviews">

| Metric Name                             | Description         | Unit  |
|:----------------------------------------|:--------------------|:------|
| appinsights.pageviews.load.milliseconds | Page view load time | ms    |
| appinsights.pageviews.total.count       | Page views          | Count |

</TabItem>
<TabItem value="Requests" label="Requests">

| Metric Name                                      | Description                        | Unit       |
|:-------------------------------------------------|:-----------------------------------|:-----------|
| appinsights.requests.duration.milliseconds       | Server response time               | ms         |
| appinsights.requests.execution.time.milliseconds | HTTP request execution time        | ms         |
| appinsights.requests.failed.count                | Failed requests                    | Count      |
| appinsights.requests.queued.count                | HTTP requests in application queue | Count      |
| appinsights.requests.http.perseconds             | HTTP request rate                  | requests/s |
| appinsights.requests.perseconds                  | Server request rate                | requests/s |
| appinsights.requests.total.count                 | Server requests                    | Count      |

</TabItem>
</Tabs>

## Prerequisites

Please find all the prerequisites needed for Centreon to get information from Azure on the [dedicated page](../getting-started/how-to-guides/azure-credential-configuration.md).

## Setup 

<Tabs groupId="sync">
<TabItem value="Online License" label="Online License">

1. Install the Centreon package on every Centreon poller expected to monitor Azure Application Insights resources:

```bash
yum install centreon-plugin-Cloud-Azure-Management-ApplicationInsights-Api
```

2. On the Centreon Web interface, install the *Azure Application Insights* Centreon Monitoring Connector on the **Configuration > Monitoring Connector Manager** page

</TabItem>
<TabItem value="Offline License" label="Offline License">

1. Install the Centreon package on every Centreon poller expected to monitor Azure Application Insights resources:

```bash
yum install centreon-plugin-Cloud-Azure-Management-ApplicationInsights-Api
```

2. Install the Centreon Monitoring Connector RPM on the Centreon Central server:

```bash
yum install centreon-pack-cloud-azure-management-applicationinsights.noarch
```

3. On the Centreon Web interface, install the *Azure Application Insights* Centreon Monitoring Connector on the **Configuration > Monitoring Connector Manager** page

</TabItem>
</Tabs>

## Configuration

### Host

* Log into Centreon and add a new Host through "Configuration > Hosts".
* In the *IP Address/FQDN* field, set the following IP address: '127.0.0.1'.

* Select the *Cloud-Azure-Management-ApplicationInsights-custom* template to apply to the Host.
* Once the template applied, some Macros marked as 'Mandatory' hereafter have to be configured.
These mandatory Macros differ regarding the custom mode used.

> Two methods can be used to set the Macros:
> * full ID of the Resource (```/subscriptions/<subscription_id>/resourceGroups/<resourcegroup_id>/providers/Microsoft.Network/<resource_type>/<resource_name>```)
in *AZURERESOURCE*
> * Resource Name in *AZURERESOURCE* associated with Resource Group (in *AZURERESOURCEGROUP*) and Resource Type (in *AZURERESOURCETYPE*)

<Tabs groupId="sync">
<TabItem value="Azure Monitor API" label="Azure Monitor API">

| Mandatory | Nom                | Description                                        |
|:----------|:-------------------|:---------------------------------------------------|
| X         | AZURECUSTOMMODE    | Custom mode 'api'                                  |
| X         | AZURESUBSCRIPTION  | Subscription ID                                    |
| X         | AZURETENANT        | Tenant ID                                          |
| X         | AZURECLIENTID      | Client ID                                          |
| X         | AZURECLIENTSECRET  | Client secret                                      |
| X         | AZURERESOURCE      | ID or name of the Application Gateway resource     |
|           | AZURERESOURCEGROUP | Associated Resource Group if resource name is used |
|           | AZURERESOURCETYPE  | Associated Resource Type if resource name is used  |

</TabItem>
<TabItem value="Azure AZ CLI" label="Azure AZ CLI">

| Mandatory | Nom                | Description                                        |
|:----------|:-------------------|:---------------------------------------------------|
| X         | AZURECUSTOMMODE    | Custom mode 'azcli'                                |
| X         | AZURESUBSCRIPTION  | Subscription ID                                    |
| X         | AZURERESOURCE      | ID or name of the Application Gateway resource     |
|           | AZURERESOURCEGROUP | Associated Resource Group if resource name is used |
|           | AZURERESOURCETYPE  | Associated Resource Type if resource name is used  |

</TabItem>
</Tabs>

## How to check in the CLI that the configuration is OK and what are the main options for ?

Once the Plugin installed, log into your Centreon Poller CLI using the *centreon-engine* 
user account and test the Plugin by running the following command:

```bash
/usr/lib/centreon/plugins/centreon_azure_management_applicationinsights_api.pl \
    --plugin=cloud::azure::management::applicationsinsights::plugin \
    --mode=requests \
    --custommode=api \
    --subscription='xxxxxxxxx' \
    --tenant='xxxxxxxxx' \
    --client-id='xxxxxxxxx' \
    --client-secret='xxxxxxxxx' \
    --resource='APP001ABCD' \
    --resource-group='RSG1234' \
    --timeframe='900' \
    --interval='PT5M' \
    --aggregation='Total' \
    --warning-requests-failed='80' \
    --critical-requests-failed='90'
```

Expected command output is shown below:

```bash
OK: Instance 'APP001ABCD' Statistic 'total' Metrics Server requests: 3266.57, HTTP request rate: 0.00requests/s, Server response time: 3266.57ms, HTTP request execution time: 0.00ms, HTTP requests in application queue: 0.00, Server request rate: 0.10requests/s, Failed requests: 0.00 | 'APP001ABCD~total#appinsights.requests.total.count'=3266.57;;;0; 'APP001ABCD~total#appinsights.requests.http.perseconds'=0.00requests/s;;;0; 'APP001ABCD~total#appinsights.requests.duration.milliseconds'=3266.57ms;;;0; 'APP001ABCD~total#appinsights.requests.execution.time.milliseconds'=0.00ms;;;0; 'APP001ABCD~total#appinsights.requests.failed.count'=0.00;;;0; 'APP001ABCD~total#appinsights.requests.server.perseconds'=0.10requests/s;;;0; 'APP001ABCD~total#appinsights.requests.failed.count'=0.00;;;0;
```

The command above checks the *requests* of an Azure *Application Insights* instance using the 'api' custom-mode
(```--plugin=cloud::azure::management::applicationsinsights::plugin --mode=requests --custommode=api```).
This Application Insights instance is identified by its id (```--resource='APP001ABCD'```) and its associated group (```--resource-group='RSG1234'```).
The authentication parameters to be used with the custom mode are specified in the options (```--subscription='xxxxxxxxx'
--tenant='xxxxxxx' --client-id='xxxxxxxx' --client-secret='xxxxxxxxxx'```).

The calculated metrics are the total values (```--aggregation='Total'```) of a 900 secondes / 15 min period (```--timeframe='900'```)
with one sample per 5 minutes (```--interval='PT5M'```).

This command would trigger a WARNING alarm if the number of *failed* requests is reported as over 80 (```--warning-requests-failed='80'```)
and a CRITICAL alarm over 90 *failed* requests (```--critical-requests-failed='90'```).

All the available options for a given mode can be displayed by adding the ```--help``` parameter to the command:

```bash
/usr/lib/centreon/plugins/centreon_azure_management_applicationinsights_api.pl \
    --plugin=cloud::azure::management::applicationsinsights::plugin \
    --mode=requests \
    --help
```

## Troubleshooting

### The Azure credentials have changed and the Plugin does not work anymore

The Plugin is using a cache file to keep connection information and avoid an authentication at each call. 
If some of the authentication parameters change, you must delete the cache file. 

The cache file can be found within  ```/var/lib/centreon/centplugins/``` folder with a name similar to azure_api_`<md5>_<md5>_<md5>_<md5>`.

### ```UNKNOWN: Login endpoint API returns error code 'ERROR_NAME' (add --debug option for detailed message)```

This error message means that some parameters used to authenticate the API request are wrong. The 'ERROR_NAME' string gives 
some hints about where the problem stands. 

As an example, if my Client ID or Client Secret are wrong, 'ERROR_DESC' value will be 'invalid_client'. 

### ```UNKNOWN: 500 Can't connect to login.microsoftonline.com:443```

This error message means that the Centreon Plugin couldn't successfully connect to the Azure Login API. Check that no third party
device (such as a firewall) is blocking the request. A proxy connection may also be necessary to connect to the API.
This can be done by using this option in the command: ```--proxyurl='http://proxy.mycompany:8080'```.

### ```UNKNOWN: No metrics. Check your options or use --zeroed option to set 0 on undefined values```

This command result means that Azure does not have any value for the requested period.
This result can be overriden by adding the ```--zeroed``` option in the command. This will force a value of 0 when no metric has
been collected and will prevent the UNKNOWN error message.
