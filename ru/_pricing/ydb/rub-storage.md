### Хранилище и резервные копии {#prices-storage}

Услуга | Цена за ГБ в месяц | |
----- | ----- | -----
| | **До 12 апреля 2022 включительно** | **С 13 апреля 2022** |
Хранение данных на группах хранения из SSD-накопителей | {{ sku|RUB|ydb.cluster.v1.ssd|month|string }} | 21,46 ₽
Хранение резервных копий по требованию в {{ objstorage-full-name }} | 1,2610 ₽ | 2,01 ₽

{% note info "Минимальный размер группы" %}

Одна [группа хранения](../../ydb/concepts/databases.md#storage-groups) позволяет разместить до 100 Гб пользовательских данных. Минимальная гранулярность выделения места для базы данных – одна группа хранения.

{% endnote %}
