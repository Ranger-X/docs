---
sourcePath: ru/_cli-ref/cli-ref/managed-services/compute/placement-group/create.md
---
# yc compute placement-group create

Create a placement group

#### Command Usage

Syntax: 

`yc compute placement-group create <PLACEMENT-GROUP-NAME> [Flags...] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--name`|<b>`string`</b><br/> A name of the placement group.|
|`--description`|<b>`string`</b><br/> A textual description of the placement group.|
|`--labels`|<b>`key=value[,key=value...]`</b><br/> A list of label KEY=VALUE pairs to add.|
|`--spread-strategy`| Use spread placement strategy.|
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
