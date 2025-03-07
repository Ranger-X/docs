#### Квоты {#mch-quotas}

| Вид ограничения                                                                | Значение |
|:-------------------------------------------------------------------------------|:---------|
| Количество кластеров в одном облаке                                            | 16       |
| Суммарное количество ядер процессора для всех хостов баз данных в одном облаке | 96       |
| Суммарный объем виртуальной памяти для всех хостов баз данных в одном облаке   | 640 ГБ   |
| Суммарный объем хранилищ для всех кластеров в одном облаке                     | 4096 ГБ  |


#### Лимиты {#mch-limits}

| Вид ограничения                                                                                                      | Минимальное значение                                                                            | Максимальное значение                            |
|:---------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------|:-------------------------------------------------|
| Класс хоста                                                                                                          | b1.nano ([5%](../../compute/concepts/performance-levels.md) × 2 vCPU Intel Broadwell, 2 ГБ RAM) | m3-c80-m640 (80 vCPU Intel Ice Lake, 640 ГБ RAM) |
| Количество хостов {{ CH }} в нешардированном кластере при использовании стандартного или быстрого сетевого хранилища | 1                                                                                               | 7                                                |
| Количество хостов {{ CH }} в нешардированном кластере при использовании нереплицируемого сетевого хранилища          | 3                                                                                               | 7                                                |
| Количество хостов {{ CH }} в нешардированном кластере при использовании локального хранилища                         | 2                                                                                               | 7                                                |
| Количество шардов в шардированном кластере                                                                           | 1                                                                                               | 50                                               |
| Количество хостов в шарде при использовании стандартного или быстрого сетевого хранилища                             | 1                                                                                               | 7                                                |
| Количество хостов в шарде при использовании нереплицируемого сетевого хранилища                                      | 3                                                                                               | 7                                                |
| Количество хостов в шарде при использовании локального хранилища                                                     | 2                                                                                               | 7                                                |
| Общее количество хостов в одном кластере                                                                             | 1                                                                                               | 353 (50 шардов × 7 хостов + 3 хоста {{ ZK }})    |
| Объем данных на хосте при использовании стандартного или быстрого сетевого хранилища                                 | 10 ГБ                                                                                           | 4096 ГБ                                          |
| Объем данных на хосте при использовании нереплицируемого сетевого хранилища                                          | 93 ГБ                                                                                           | 8184 ГБ                                          |
| Объем данных на хосте при использовании локального хранилища (для платформ Intel Broadwell и Intel Cascade Lake)     | 100 ГБ                                                                                          | 1500 ГБ                                          |
| Объем данных на хосте при использовании локального хранилища (для платформы Intel Ice Lake)                          | {{ local-ssd-v3-step }}                                                                         | {{ local-ssd-v3-max }}                           |
