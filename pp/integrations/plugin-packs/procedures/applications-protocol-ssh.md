---
id: applications-protocol-ssh
title: Protocol SSH
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Overview

The Secure Shell Protocol (SSH) is a secure network protocol for remote actions
from one computer to another.

The Centreon Monitoring Connector *Protocol SSH* aims to collect the status and response 
time of a SSH server login.

## Pack assets

### Monitored objects

* SSH server

### Collected metrics & status

<Tabs groupId="sync">
<TabItem value="Ssh-Login" label="Ssh-Login">

| Metric name           | Description         | Unit       |
|:----------------------|:--------------------|:-----------|
| status                | Login status        |            |
| response.time.seconds | Login response time | seconds    |


</TabItem>
</Tabs>

## Prerequisites

To use this pack, the SSH service must be properly configured on your server and
the mandatory Host Macros must be properly configured. More info in the 
"Configuration" section [here](#Host).

## Setup

<Tabs groupId="sync">
<TabItem value="Online License" label="Online License">

1. Install the Centreon package on every Centreon poller expected to monitor a SSH server:

```bash
yum install centreon-plugin-Applications-Protocol-Ssh
```

2. On the Centreon Web interface, install the *Protocol SSH* Centreon Monitoring Connector on the **Configuration > Monitoring Connector Manager** page

</TabItem>
<TabItem value="Offline License" label="Offline License">

1. Install the Centreon package on every Centreon poller expected to monitor a SSH server:

```bash
yum install centreon-plugin-Applications-Protocol-Ssh
```

2. Install the *Protocol SSH* Centreon Monitoring Connector RPM on the Centreon Central server:

```bash
yum install centreon-pack-applications-protocol-ssh
```

3. On the Centreon Web interface, install the *Protocol SSH* Centreon Monitoring Connector on the **Configuration > Monitoring Connector Manager** page

</TabItem>
</Tabs>

## Configuration

### Host

* Log into Centreon and add a new Host through "Configuration > Hosts".
* Fill the "Name", "Alias" & "IP Address / DNS" fields according to your SSH server settings
* Select the *Applications-Protocol-Ssh-custom* template to apply to the Host
* Once the template applied, some Macros marked as 'Mandatory' hereafter have to be configured.

| Mandatory | Name                | Description                                                                        |
|:----------|:--------------------|:-----------------------------------------------------------------------------------|
| X         | PROTOCOLSSHPASSWORD |                                                                                    |
| X         | PROTOCOLSSHUSERNAME |                                                                                    |
|           | EXTRAOPTIONS        | Any extra option you may want to add to every command\_line (eg. a --verbose flag) |

## How to check in the CLI that the configuration is OK and what are the main options for ? 

Once the plugin installed, log into your Centreon Poller CLI using the 
*centreon-engine* user account and test the Plugin by running the following 
command:

```bash
 /usr/lib/centreon/plugins//centreon_protocol_ssh.pl  \
    --plugin=apps::protocols::ssh::plugin  \
    --mode=login  \
    --hostname=10.0.0.1   \
    --ssh-username=''  \
    --ssh-password=''  \
    --warning-status=''  \
    --critical-status='%{message} !~ /authentification succeeded/i'  \
    --warning-time='2'  \
    --critical-time='3'  \
    --use-new-perfdata 
 ```

 Expected command output is shown below:

 ```bash
OK : authentification succeeded | 'response.time.seconds'=1s;;;; 
 ```

This command would trigger a WARNING alarm if the login response time is 
reported as over 2 seconds (```--warning-time='2'```) and a CRITICAL alarm 
over 3 seconds (```--critical-time='3'```) or if the login status if different
than "authentification succeeded" 
(```--critical-status='%{message} !~ /authentification succeeded/i''```).

All available options for a given mode can be displayed by adding the 
```--help``` parameter to the command:

 ```bash
 /usr/lib/centreon/plugins//centreon_protocol_ssh.pl  \
    --plugin=apps::protocols::ssh::plugin  \
    --mode=login  \
    --help
 ```

All available options for a given mode can be displayed by adding the 
```--list-mode``` parameter to the command:

```bash
 /usr/lib/centreon/plugins//centreon_protocol_ssh.pl  \
    --plugin=apps::protocols::ssh::plugin  \
    --list-mode
 ```

### Troubleshooting

#### ```UNKNOWN: Command error: Host key verification failed.```

This error means means you haven't manually validated the target server 
fingerprint with ```ssh``` or ```plink``` on the Centreon poller.