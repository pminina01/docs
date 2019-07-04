#### Для чего нужны tablet slaves
Хотя у таблетки должно существовать не более одного активного мастера, иногда полезно поддерживать дополнительно несколько реплик-слейвов. Этим можно решить одну из нескольких задач:
  * уменьшить время переподъема таблетки (при переключении на тёплую реплику понадобится только перерегистрировать мастера и накатить изменения, не успевшие доехать асинхронной доставкой).
  * в случае, когда допустимы "отстающие" чтения
    * вынести обработку читающих транзакций с мастера - увеличив пропускную способность системы.
    * читать с локальных реплик в меж-ДЦ инсталляциях.
    * сохранять доступность на чтение во время рестарта мастера.

#### Реализация на системного уровне 
При запуске таблетки (либо явной командой с **[Hive'a](tablet_hive.md)**, либо указав возможность запуска слейвов в **[bootstrapper](glossary.md#bootstrapper)**) можно назначить новый инстанс таблетки не кандидатом, а слейвом.

  * Инстанс слейва находит текущий мастер и регистрирует себя как нового слейва.
  * Следующий после этого снапшот лога будет отправлен мастером на слейв (рекомендуется принудительно сбрасывать снапшот лога таблеткой при подключении нового слейва).
  * Получив снапшот лога слейв осуществляет стандартную процедуру загрузки, но не фиксирует состояние в сторадже, вместо этого регистрирует себя как активного слейва в стейт-сторадже (необходимо для работы пайпов).
  * Весь дальнейший лог транслируется мастером на слейвов, а слейвы применяют изменения к состоянию в памяти.

Логи перестают отгружаться при разрыве линка между мастером и слейвом, в этом случае слейв пытается перерегистрировать себя на мастере (не делая различия между новым и старым) и проходит процедуру загрузки снашпота лога с начала. На время перерегистрации слейв может сохранять накопленный стейт и обслуживать запросы базируясь на нём.

При обслуживании чтений слейвам может понадобиться загрузить данные с диска, полученные фрагменты складываются в локальном кеше и могут быть переиспользованы при апгрейде слейва до мастера. Альтернативно профиль запросов может отгружаться с мастера на слейвов для синхронизации состояния кеша (полезно при использовании слейва как hot-standby).

Обращения к слейвам происходят тем же механизмом таблеточных пайпов, что и к мастеру, но с включенной опцией разрешения/требования доступа к слейвам.

#### Реализация на уровне PQ-топиков 
Не поддерживается.

#### Реализация на уровне таблиц 
Должно поддерживаться даташардами с настройкой на уровне таблиц.