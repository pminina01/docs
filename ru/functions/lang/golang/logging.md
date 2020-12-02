# Журналирование

Сервис {{ sf-name }} автоматически захватывает потоки стандартного вывода приложения и отправляет их в централизованную систему журналирования, доступную в {{ yandex-cloud }}. Помимо журналов выполнения приложения записываются системные записи о событиях выполнения запроса.

Для записи дополнительных сообщений используются стандартные языковые конструкции:
1. `fmt.Print` / `Println` — выводит сообщение в стандартный поток вывода `stdout`.
1. `print` / `println` — выводит сообщение в стандартный поток ошибок `stderr`.
1. `time.Now` + `time.Since` — возвращает продолжительность выполнения действия.

{% include [multiline warning](../../../_includes/functions/multiline.md) %}

Более подробно со спецификацией форматирования строк можно ознакомиться в [соответствующем разделе документации](https://golang.org/pkg/fmt/). О встроенных функциях `print` и `println` можно почитать [здесь](https://golang.org/pkg/builtin/), а о пакете `time` и его возможностях [здесь](https://golang.org/pkg/time/).

{% include [router-logging](../../../_includes/functions/router-logging.md) %} 