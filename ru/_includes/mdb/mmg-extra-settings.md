- **Начало резервного копирования (UTC)**{#setting-backup-start}

  Время по UTC (в 24-часовом формате), когда начинается [резервное копирование](../../managed-mongodb/operations/cluster-backups.md) кластера. Если время не задано, резервное копирование начнется в 22:00 UTC.

- **Срок хранения автоматических резервных копий, дней**{#setting-backup-saving}
  
  Время, в течение которого нужно хранить созданные автоматически резервные копии. Если для такой копии истекает срок хранения, то она удаляется. Значение по умолчанию — {{ mmg-backup-retention }} дней. Эта функциональность находится на стадии [Preview](../../overview/concepts/launch-stages.md). Подробнее см. в разделе [{#T}](../../managed-mongodb/concepts/backup.md).

  Изменение срока хранения затрагивает как новые автоматические резервные копии, так и уже существующие. Например, если изначальный срок хранения был 7 дней и оставшееся время жизни отдельной автоматической резервной копии при таком сроке — 1 день, то при увеличении срока хранения до 9 дней, оставшееся время жизни этой резервной копии будет уже 3 дня.

- **Окно обслуживания**{#setting-maintenance-window}

  Настройки времени технического обслуживания:
  - Чтобы указать предпочтительное время начала обслуживания хостов кластера, выберите пункт по **по расписанию** и укажите нужные день недели и час дня в UTC (Coordinated Universal Time).
  - Чтобы разрешить проведение технического обслуживания в любое время, выберите пункт **произвольное**.

  К техническому обслуживанию относится обновление версии СУБД, применение патчей и так далее.

- **Сбор статистики** — включите эту опцию, чтобы воспользоваться инструментом [{#T}](../../managed-mongodb/operations/performance-diagnostics.md) в кластере. Эта функциональность находится на стадии [Preview](../../overview/concepts/launch-stages.md).

- **Защита от удаления** — включите эту опцию, чтобы защитить кластер от непреднамеренного удаления пользователем вашего облака.

    {% include [Ограничения защиты от удаления](../../_includes/mdb/deletion-protection-limits-db.md) %}
