---
sourcePath: ru/_cli-ref/cli-ref/managed-services/managed-redis/cluster/restore.md
---
# yc managed-redis cluster restore

Restore Redis cluster

#### Command Usage

Syntax: 

`yc managed-redis cluster restore [Flags...] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--backup-id`|<b>`string`</b><br/> ID of the backup to create a cluster from.|
|`--name`|<b>`string`</b><br/> Cluster name.|
|`--description`|<b>`string`</b><br/> Cluster description.|
|`--environment`|<b>`string`</b><br/> Cluster environment. Values: production, prestable.|
|`--network-id`|<b>`string`</b><br/> Network id.|
|`--network-name`|<b>`string`</b><br/> Network name.|
|`--host`|<b>`PROPERTY=VALUE[,PROPERTY=VALUE...]`</b><br/> Individual configurations for hosts that should be created for the Redis cluster.  Possible property names:  zone-id ID of the availability zone where the host resides.  subnet-id ID of the subnet that the host should be created in.  subnet-name Name of the subnet that the host should be created in.  |
|`--redis-version`|<b>`string`</b><br/> Version of Redis used in the cluster. Values: 5.0, 6.0, 6.2|
|`--password`|<b>`string`</b><br/> Authentication password.|
|`--max-memory-policy`|<b>`string`</b><br/> Redis maxmemory setting. Values: 'volatile-lru', 'allkeys-lru', 'volatile-lfu', 'allkeys-lfu', 'volatile-random', 'allkeys-random', 'volatile-ttl', 'noeviction'|
|`--timeout`|<b>`int`</b><br/> Time seconds that Redis keeps the connection open while the client is idle.|
|`--notify-keyspace-events`|<b>`string`</b><br/> Redis events to notify about.|
|`--slowlog-max-len`|<b>`int`</b><br/> Maximum length of slow operations log.|
|`--slowlog-log-slower-than`|<b>`int`</b><br/> Threshold in milliseconds to log slow operations.|
|`--databases`|<b>`int`</b><br/> Number of Redis databases.|
|`--resource-preset`|<b>`string`</b><br/> ID of the preset for computational resources available to a host (CPU, memory etc.).|
|`--disk-size`|<b>`byteSize`</b><br/> Volume of the storage available to a host.|
|`--disk-type-id`|<b>`string`</b><br/> Disk type id (e.g., network-ssd).|
|`--backup-window-start`|<b>`timeofday`</b><br/> Start time for the daily backup in UTC timezone. Format: HH:MM:SS|
|`--datalens-access`| Allow access for DataLens|
|`--labels`|<b>`key=value[,key=value...]`</b><br/> A list of label KEY=VALUE pairs to add.|
|`--enable-tls`| Enables tls for Redis cluster.|
|`--security-group-ids`|<b>`value[,value]`</b><br/> A list of security groups for the Redis cluster.|
|`--async`| Display information about the operation in progress, without waiting for the operation to complete.|

#### Flags

| Flag | Description |
|----|----|
|`--profile`|<b>`string`</b><br/>Set the custom configuration file.|
|`--debug`|Debug logging.|
|`--debug-grpc`|Debug gRPC logging. Very verbose, used for debugging connection problems.|
|`--no-user-output`|Disable printing user intended output to stderr.|
|`--retry`|<b>`int`</b><br/>Enable gRPC retries. By default, retries are enabled with maximum 5 attempts. Pass 0 to disable retries. Pass any negative value for infinite retries. Even infinite retries are capped with 2 minutes timeout.|
|`--cloud-id`|<b>`string`</b><br/>Set the ID of the cloud to use.|
|`--folder-id`|<b>`string`</b><br/>Set the ID of the folder to use.|
|`--folder-name`|<b>`string`</b><br/>Set the name of the folder to use (will be resolved to id).|
|`--token`|<b>`string`</b><br/>Set the OAuth token to use.|
|`--format`|<b>`string`</b><br/>Set the output format: text (default), yaml, json, json-rest.|
|`-h`,`--help`|Display help for the command.|
