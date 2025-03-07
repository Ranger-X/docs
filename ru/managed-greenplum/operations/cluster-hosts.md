# Управление хостами кластера

Вы можете получить список хостов (мастеров и сегментов) в кластере {{ mgp-name }}.

## Получить список хостов в кластере {#list}

{% list tabs %}

* Консоль управления

    1. Перейдите на страницу каталога и выберите сервис **{{ mgp-name }}**.
    1. Нажмите на имя нужного кластера, затем выберите вкладку **Хосты**.

{% endlist %}

В списке хостов в колонке **Роль** указывается роль каждого хоста:

* `MASTER` — первичный хост-мастер (PRIMARY). Принимает пользовательские подключения.
* `REPLICA` — резервный хост-мастер (STANDBY). Реплицирует данные первичного хоста-мастера.
* `SEGMENT` — хост-сегмент. Хранит часть данных кластера.

{% include [greenplum-trademark](../../_includes/mdb/mgp/trademark.md) %}
