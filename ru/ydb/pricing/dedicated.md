---
editable: false
---

# Правила тарификации для режима {{ ydb-name }} с выделенными инстансами

{% include [currency-choice](../_includes/pricing/currency-choice.md) %}

{% include [pricing-status.md](../_includes/pricing/pricing-status.md) %}

## Из чего складывается стоимость использования YDB {#rules}

При работе {{ ydb-name }} в режиме с выделенными инстансами вы оплачиваете:

* тип и размер [групп хранения](../concepts/databases.md#storage-groups), выделенных для базы данных;
* вычислительные ресурсы, выделенные базе данных.

Дополнительно оплачиваются иные потребляемые ресурсы:

* место, занятое в сервисе {{ objstorage-name }} для хранения резервных копий по требованию;
* объем исходящего трафика из {{ yandex-cloud }} в интернет.


{% include [pricing-gb-size](../_includes/pricing/pricing-gb-size.md) %}

### Использование вычислительных ресурсов {#rules-hosts-uptime}

Стоимость начисляется за каждый час работы виртуальной машины в соответствии с ее классом. Точные характеристики классов приведены в разделе [Основные понятия](../concepts/databases.md#compute-units).

Минимальная единица тарификации — час (например, стоимость 1,5 часов работы виртуальной машины равна стоимости 2 часов).

### Использование дискового пространства {#rules-storage}

Оплачивается:

* Объем хранилища, выделенный для групп хранения базы данных.

* Объем, занимаемый резервными копиями баз данных по требованию, сохраненными в сервисе {{ objstorage-name }}.

   {% note info %}

   Yandex Database для каждой базы автоматические создает и бесплатно хранит 2 полные резервные копии за два последних дня. Плата за хранение автоматических резервных копий не взимается.

   {% endnote %}

Цена указывается за 1 месяц использования. Минимальная единица тарификации — 1 ГБ в час (например, стоимость хранения 1 ГБ в течение 1,5 часов равна стоимости хранения в течение 2 часов).

## Скидка за резервируемый объем ресурсов (CVoS) {#cvos}

Вы можете получить гарантированную скидку за потребление ресурсов сервиса, запланированное на месяц, на год или на три года вперед.

Сервис Yandex Database предоставляет [CVoS](../../billing/concepts/cvos.md) двух видов: на vCPU и RAM для хостов, составляющих базу данных. В консоли управления вы можете увидеть потенциальную экономию для текущего потребления ресурсов при переводе их на схему CVoS, а также предварительно рассчитать месячные платежи для баз данных, использующих виртуальные машины определенного класса.

{% note info %}

По схеме CVoS можно заказать только ресурсы определенного вида: для недоступных видов ресурсов в колонках CVoS в разделе [Цены](#prices) стоят прочерки. Объем хранилища и интернет-трафика заказать таким образом пока невозможно.

{% endnote %}


## Цены {#prices}

Все цены указаны с включением НДС. Цены за месяц указаны из расчета для месяца в 30 календарных дней. Для более коротких месяцев цена соответственно выше, для более длинных — ниже.

### Вычислительные ресурсы хостов {#prices-compute-units}


{% include notitle [rub-compute-units.md](../../_pricing/ydb/rub-compute-units.md) %}



### Хранилище и резервные копии {#prices-storage}


{% include notitle [rub-storage.md](../../_pricing/ydb/rub-storage.md) %}



### Исходящий трафик {#prices-traffic}


{% include notitle [rub-egress-traffic.md](../../_pricing/rub-egress-traffic.md) %}



## Расчетные цены для вычислительных ресурсов {#calculated-prices}


{% include notitle [rub-dedicated.md](../../_pricing/ydb/rub-dedicated.md) %}
