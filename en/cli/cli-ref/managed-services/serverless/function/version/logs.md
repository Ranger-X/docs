---
sourcePath: en/_cli-ref/cli-ref/managed-services/serverless/function/version/logs.md
---
# yc serverless function version logs

Read function version logs

#### Command Usage

Syntax: 

`yc serverless function version logs [--id] <VERSION-ID> [--since <SINCE>] [--until <UNTIL>] [--follow|-f] [Global Flags...]`

#### Global Flags

| Flag | Description |
|----|----|
|`--id`|<b>`string`</b><br/>Function version id.|
|`--limit`|<b>`int`</b><br/>The maximum number of items to list.|
|`--since`|<b>`timestamp`</b><br/>Show logs since this time|
|`--until`|<b>`timestamp`</b><br/>Show logs until this time|
|`-f`,`--follow`|Output logs as they arrive|

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
