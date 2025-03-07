---
sourcePath: ru/_cli-ref/cli-ref/managed-services/serverless/function/set-scaling-policy.md
---
# yc serverless function set-scaling-policy

Set scaling policy for specified function and tag

#### Command Usage

Syntax: 

`yc serverless function set-scaling-policy <FUNCTION-NAME>|<FUNCTION-ID> [--tag <TAG>] [Flags...] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--tag`|<b>`string`</b><br/> Version tag|
|`--zone-instances-limit`|<b>`int`</b><br/> Upper limit for instance count in each zone|
|`--zone-requests-limit`|<b>`int`</b><br/> Upper limit for requests count in each zone|
|`--provisioned-instances-count`|<b>`int`</b><br/> Provisioned instances count in each zone|
|`--id`|<b>`string`</b><br/> Function id.|
|`--name`|<b>`string`</b><br/> Function name.|
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
