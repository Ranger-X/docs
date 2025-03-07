### Licenses {#licence}

For the following products, funds are debited once for the calendar month in advance when a VM is started, regardless of the actual amount of time the VM runs for:

| Resource | Cost per vCPU per month, without VAT
| --- | ---
| Windows Server Datacenter | $11.7144
| Microsoft SQL Server Standard | $75.59615
| Microsoft SQL Server Enterprise | $258.50001

### Host computing resources {#prices-hosts}

| Resource       | Cost for 1 hour, without VAT                       |
|----------------|----------------------------------------------------|
| **Intel Cascade Lake**                                              |
| 100% vCPU      | {{ sku|USD|mdb.cluster.mssql.v2.cpu.c100|string }} |
| RAM (for 1 GB) | {{ sku|USD|mdb.cluster.mssql.v2.ram|string }}      |
| **Intel Ice Lake**                                                  |
| 100% vCPU      | {{ sku|USD|mdb.cluster.mssql.v3.cpu.c100|string }} |
| RAM (for 1 GB) | {{ sku|USD|mdb.cluster.mssql.v3.ram|string }}      |

### Storage and backups {#prices-storage}

{% include [local-ssd for Ice Lake only by request](../../_includes/ice-lake-local-ssd-note.md) %}

| Service                         | Cost of 1 GB per month, without VAT                                    |
|---------------------------------|------------------------------------------------------------------------|
| Standard network storage        | {{ sku|USD|mdb.cluster.network-hdd.mssql|month|string }}               |
| Non-replicated network storage  | {{ sku|USD|mdb.cluster.network-ssd-nonreplicated.mssql|month|string }} |
| Fast network storage            | {{ sku|USD|mdb.cluster.network-nvme.mssql|month|string }}              |
| Fast local storage              | {{ sku|USD|mdb.cluster.local-nvme.mssql|month|string }}                |
| Backups beyond the storage size | $0.032594                                                              |
