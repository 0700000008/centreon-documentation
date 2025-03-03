---
id: concepts
title: Monitoring basics
---

## What does Centreon monitor?

Centreon allows you to monitor resources. Resources can be hosts or services:

* A **host** is any device that has an IP address and that one wishes to monitor.
For example, it could be a physical server, a virtual machine, a temperature probe, an IP camera, a printer or a storage space. A host can have one or more associated services.
* A **service** is a check point, or indicator, to be monitored on a host.
This can be the CPU usage rate, temperature, motion detection, bandwidth usage rate, disk I/O, etc. A service can consist of one or several metrics.

## How does monitoring work?

In order to collect each indicator value, monitoring plugins are used. These are periodically executed by a collection engine called Centreon Engine.

## How do I see the resources being monitored?

Once hosts and services are monitored, they have a status in Centreon (e.g. **OK**, **Warning**, **Critical**...). You can keep track of any changes using the **Monitoring > Resources Status** page.

If an alert occurs (not-OK/not-UP status), [contacts/users](../monitoring/basic-objects/contacts-create.md) will be able to receive [notifications](../alerts-notifications/notif-configuration.md), within set time periods.

## What features can I use to help me monitor hosts?

In Centreon, monitoring is made easy by the following elements:

* Host templates and service templates that allow you to define default values to speed up the creation of these objects.

* [Monitoring Connectors](../monitoring/pluginpacks.md) that provide ready-to-use host and service templates. These greatly simplify the configuration of hosts and services: for instance, all you have to do is to apply Monitoring Connector templates to a host for it to be monitored.

* The autodiscovery feature for hosts and services, which allows you to obtain a list of new hosts and services and add them automatically to the list of monitored resources.

## See also

To learn more about Centreon, you can also read our [**Glossary of Centreon concepts**](../resources/glossary.md).
