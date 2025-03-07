---
sourcePath: ru/_cli-ref/cli-ref/managed-services/ydb/database/index.md
---
# yc ydb database

Manage YDB databases.

#### Command Usage

Syntax: 

`yc ydb database <command>`

Aliases: 

- `db`

#### Command Tree

- [yc ydb database get](get.md) — Get information about the specified YDB database.
- [yc ydb database list](list.md) — List YDB databases in a folder.
- [yc ydb database create](create.md) — Create YDB database.
- [yc ydb database backup](backup.md) — Backup YDB database.
- [yc ydb database restore](restore.md) — Restore backup.
- [yc ydb database update](update.md) — Update the specified YDB database.
- [yc ydb database stop](stop.md) — Stop the specified YDB database.
- [yc ydb database start](start.md) — Start the specified YDB database.
- [yc ydb database delete](delete.md) — Delete the specified YDB database.
- [yc ydb database add-labels](add-labels.md) — Add labels to specified YDB database.
- [yc ydb database remove-labels](remove-labels.md) — Remove labels from specified YDB database.

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
