---
title: Yandex Database (YDB). Обзор СУБД
description: 'Yandex Database (YDB) — это горизонтально масштабируемая распределённая отказоустойчивая СУБД. YDB спроектирована с учетом требований высокой производительности — например, обычный сервер может обрабатывать десятки тысяч запросов в секунду. В дизайн системы заложена работа с объемами данных в сотни петабайт.'
sourcePath: core/concepts/_includes/index/intro.md
---


# Обзор Yandex Database (YDB)

*Yandex Database* (YDB) — это горизонтально масштабируемая распределённая отказоустойчивая СУБД. YDB спроектирована с учетом требований высокой производительности — например, обычный сервер может обрабатывать десятки тысяч запросов в секунду. В дизайн системы заложена работа с объемами данных в сотни петабайт. YDB может эксплуатироваться в однодатацентровом и геораспределенном (кросс-датацентровый) режимах на кластере из тысяч серверов.

YDB обеспечивает:

* [строгую консистентность](https://en.wikipedia.org/wiki/Consistency_model#Strict_Consistency) с возможностью ослабления для увеличения производительности;
* поддержку запросов [YQL](../../../yql/reference/index.md) (диалект SQL для работы с большими данными);
* автоматическую репликацию данных;
* высокую доступность с автоматической обработкой отказов вычислительных узлов, стоек, или зон доступности;
* автоматическое партицирование данных при увеличении их объема или увеличении нагрузки.

Для взаимодействия с YDB доступен [YDB CLI](../../../reference/ydb-cli/index.md), а также [SDK](../../../reference/ydb-sdk/index.md) для   Java, Python, Node.js, PHP и Go.

YDB поддерживает реляционную [модель данных](../../../concepts/datamodel.md) и оперирует таблицами с предопределённой схемой. Для удобства организации таблиц поддерживается создание директорий по аналогии с файловой системой.

В качестве основного способа формирования команд к базе данных используется язык YQL, являющийся диалектом SQL. Таким образом, пользователю предлагается мощный и, в то же время, привычный способ взаимодействия с БД.

В YDB поддерживаются высокопроизводительные распределенные [ACID](https://en.wikipedia.org/wiki/ACID_(computer_science))-транзакции, которые могут затрагивать несколько записей из разных таблиц. Обеспечивается самый строгий уровень изоляции транзакций — serializable. Также имеется возможность ослабления уровня изоляции для увеличения производительности.

В дизайн YDB заложена поддержка разных сценариев нагрузки, таких как [OLTP](https://en.wikipedia.org/wiki/Online_transaction_processing) и [OLAP](https://en.wikipedia.org/wiki/Online_analytical_processing). В текущей реализации поддержка аналитических запросов ограничена. Поэтому можно говорить, что в данный момент YDB — это OLTP-база данных.

YDB используется в сервисах Яндекса в качестве высокопроизводительной [OLTP](https://en.wikipedia.org/wiki/Online_transaction_processing) СУБД. В частности, сервисы Yandex.Cloud Yandex Object Storage и Yandex Block Storage используют YDB для хранения данных и базируются на её компонентах.