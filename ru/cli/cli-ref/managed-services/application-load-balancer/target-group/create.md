---
sourcePath: ru/_cli-ref/cli-ref/managed-services/application-load-balancer/target-group/create.md
---
# yc application-load-balancer target-group create

Create a target group

#### Command Usage

Syntax: 

`yc application-load-balancer target-group create <TARGET-GROUP-NAME> [Flags...] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--name`|<b>`string`</b><br/> A name of the target group.|
|`--description`|<b>`string`</b><br/> A description of the target group.|
|`--labels`|<b>`key=value[,key=value...]`</b><br/> A list of label KEY=VALUE pairs to add.|
|`--target`|<b>`PROPERTY=VALUE[,PROPERTY=VALUE...]`</b><br/> List of targets.  Possible property names:  subnet-id Subnet id.  subnet-name Subnet name.  ip-address IP Address.  private-ip-address Private IPv4 address.  |
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
