---
sourcePath: en/_cli-ref/cli-ref/managed-services/iot/registry/list-device-topic-aliases.md
---
# yc iot registry list-device-topic-aliases

List all topic aliases set for devices in this registry

#### Command Usage

Syntax: 

`yc iot registry list-device-topic-aliases <REGISTRY-NAME>|<REGISTRY-ID> [Flags...] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--limit`|<b>`int`</b><br/>The maximum number of items to list.|
|`--id`|<b>`string`</b><br/>Registry id.|
|`--name`|<b>`string`</b><br/>Registry name.|

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
