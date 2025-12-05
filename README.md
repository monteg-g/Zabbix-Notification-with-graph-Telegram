# <p align="center">Zabbix Notification with graph to Telegram
<p align="center">Нотификатор оповещений в Telegram для <a href="https://www.zabbix.com/features#notification target="_blank"" >Zabbix 7</a>.<br>
Легкая установка, гибкая настройка, информативные сообщения.
<p align="center"><a href="https://www.zabbix.com/integrations/telegram#tab:3rd_party" target="_blank">Popular на www.zabbix.com</a> и <a href="https://share.zabbix.com/zabbix-tools-and-utilities/cat-notifications/zabbix-notification-telegram">share.zabbix.com</a>
<br>

* [Возможности](#возможности)
* [Установка]
* [Создаем первое оповещение](#создаем-первое-оповещение)
  * [Получаем API token](#получаем-api-token)
* [Настраиваем нотификатор](#настраиваем-нотификатор)
  * [Конфигурационный файл](#конфигурационный-файл)
  * [XML разметка](#xml-разметка)
  * [Тэги ZNTSettings](#тэги-zntsettings)
* [Логирование](#логирование)
* [F.A.Q.](#faq)
* [Последние значимые изменения](#последние-значимые-изменения)
* [Помощь](#помощь)

## Возможности
- Графики, информативные заголовки, ссылки<a href="#note1" id="note1ref"><sup>1</sup></a>, тэги<a href="#note2" id="note2ref"><sup>2</sup></a> и упоминания объединены в **одно сообщение**.
- Формирование и обновление cash файла (privat, group, group -> supergroup)<a href="#note3" id="note3ref"><sup>3</sup></a>
- Гибкая настройка через конфигурационный файл, XML разметку в <a href="https://www.zabbix.com/documentation/current/manual/config/notifications/action" target="_blank">действиях триггеров</a> и Trigger Tags<a href="#note4" id="note4ref"><sup>4</sup></a>
- Маппинг Emoji статуса и важности события.
- Обьединение графиков в альбом.


## Создаем первое оповещение
### Получаем API token
Получили <a href="https://core.telegram.org/bots#botfather" target="_blank">API token от @BotFather</a> который будем использовать в <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py" target="_blank">zbxTelegram_config.py</a>: <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L19" target="_blank">tg_token</a>.

*Если у Вас нет бота, я расскажу как это сделать:* <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/wiki/Регистрация-нового-бота-в-Telegram" target="_blank">RU</a>, ENG (vacant)

## Настраиваем нотификатор
### Конфигурационный файл
Основная конфигурация нотификатора производится через файл [zbxTelegram_config.py](https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py). 

Давайте разберем каждый параметр подробно:

### XML разметка
Дополнительная конфигурация производится через XML разметку([пример](https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/actions.example)) в <a href="https://www.zabbix.com/documentation/current/manual/config/notifications/action" target="_blank">Zabbix Action</a>.

Также разберем эти параметры:
|Имя|Аргумент(ы)|Описание|По умолчанию|
|---|-----------|--------|------------|
|```<messages></messages>```|string||<a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/actions.example#L4" target="_blank">Default</a>|
|```<graphs></graphs>```|bool|Добавление изображения графика в сообщение.|True|
|```<hostlinks></hostlinks>```|bool|Добавление линка на "Узел сети" (host) в сообщение.|True|
|```<graphlinks></graphlinks>```|bool|Добавление линка на график "Элемент данных" (item) в сообщение.|True|
|```<triggerlinks></triggerlinks>```|bool|Добавление линка из триггера в сообщение.|True|
|```<tag></tag>```|bool|Добавление всех тэгов в сообщение.|True|
|```<eventtag></eventtag>```|bool|Добавление тэгов события в сообщение.|True|
|```<eventidtag></eventidtag>```|bool|Добавление тэгa c eventid в сообщение.|True|
|```<itemidtag></itemidtag>```|bool|Добавление тэгa c itemid в сообщение.|True|
|```<triggeridtag></triggeridtag>```|bool|Добавление тэгa c triggerid в сообщение.|True|
|```<actionidtag></actionidtag>```|bool|Добавление тэгa c actionid в сообщение.|True|
|```<hostidtag></hostidtag>```|bool|Добавление тэгa c hostid в сообщение.|True|
|```<zntsettingstag></zntsettingstag>```|bool||True|
|```<zntmentions></zntmentions>```|bool||True|
|```<keyboard></keyboard>```|bool|Добавление кнопок к сообщению.<br>(*В стадии разработки*).|True|
|```<graphs_period></graphs_period>```|string|Период за который присылается изображение графика в секундах.|10800|
|```<host></host>```|string|Макрос имени узла сети.|{HOST.HOST}|
|```<itemid></itemid>```|string|Макросы ИД элементов данных.|{ITEM.ID1} {ITEM.ID2} {ITEM.ID3} {ITEM.ID4}|
|```<triggerid></triggerid>```|string|Макрос ИД триггера.|{TRIGGER.ID}|
|```<eventid></eventid>```|string|Макрос ИД события.|{EVENT.ID}|
|```<actionid></actionid>```|string|Макрос ИД действия.|{ACTION.ID}|
|```<hostid></hostid>```|string|Макрос ИД узла сети.|{HOST.ID}|
|```<title><![CDATA[]]></title>```|string|Шаблон формирования заголовка изображения графика из макросов: имя узла сети и имя события.|{HOST.HOST} - {EVENT.NAME}|
|```<triggerurl><![CDATA[]]></triggerurl>```|string|Макрос URL триггера.|{TRIGGER.URL}|
|```<eventtags><![CDATA[]]></eventtags>```|string|Макрос тэгов события разделенных запятой. Макрос объединяет теги из узла сети, шаблона, триггера.|{EVENT.TAGS}|

*<a href="https://www.zabbix.com/documentation/current/ru/manual/appendix/macros/supported_by_location" target="_blank">Полный список поддерживаемых макросов в Zabbix</a>*

```<![CDATA[]]>```:
_В XML документах фрагмент, помещенный внутрь CDATA, — это часть содержания элемента, которая помечена для парсера как содержащая только символьные данные, а не разметку. CDATA — это просто альтернативный синтаксис для отображения символьных данных, нет никакой смысловой разницы между символьными данными, которые объявлены как CDATA и символьными данными, которые объявлены в обычном синтаксисе и где «<» и «>» будут представлены как «&lt;» и «&gt;», соответственно. (<a href="https://ru.wikipedia.org/wiki/CDATA" target="_blank">Wikipedia</a>)_

### Тэги ZNTSettings+ 
Более детальную настройку нотификатора можно произвести через тэги в <a href="https://www.zabbix.com/documentation/current/ru/manual/config/event_correlation/trigger/event_tags" target="_blank">триггерах</a>.

Разберем эти параметры:
|Имя|Описание|По умолчанию|
|---|--------|------------|
|trigger_settings_tag|Имя тэга для обработки значений параметров.|'ZNTSettings'|
|trigger_settings_tag_no_graph|Значение тэга 'ZNTSettings' при котором изображение графика не будет добавлено в сообщение.|'no_graph'|
|trigger_settings_tag_no_alert|Значение тэга 'ZNTSettings' при котором сообщение отправлено не будет.<br>*В [лог файл](#логирование) будет добавлено событие об отмене отправки сообщения.*|'no_alert'|
|trigger_settings_tag_not_notify|Значение тэга 'ZNTSettings' при котором сообщение будет отправляет беззвучно.<br>*Пользователи iOS не получат уведомления, пользователи Android получат уведомление без звука.*|'not_notify'|
|trigger_settings_tag_graph_normal||'graph_normal'|
|trigger_settings_tag_graph_stacked||'graph_stacked'|
|trigger_settings_tag_graph_pie||'graph_pie'|
|trigger_settings_tag_graph_exploded||'graph_exploded'|
|trigger_settings_tag_graph_period|Значение тэга 'ZNTSettings' при котором будет задан период за какой присылать изображение графика. Указывается после разделителя ```=``` в секундах.<br>Приоритет: tag, xml, config*|'period='|

|Имя|Описание|По умолчанию|
|---|--------|------------|
|trigger_info_mentions_tag|Тэг упоминания юзера|'ZNTMentions'|

<details><summary>Пример:</summary>
  <img src="https://i.imgur.com/vKQWZ7V.png" alt="Kitten"	title="A cute kitten" width="100%"/>
</details>


## Логирование

Все основные события (отправка, добавления в cash файл, изменение группы в суппергруппу, ошибки, дебаг) логируются в файле ```znt.log```, Вы можете его найти по умолчанию ```/usr/lib/zabbix/alertscripts/zbxTelegram_files/znt.log``` (<a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L15" target="_blank">config_log_file</a>])
Поддерживаются три режима логирования:
1. Обычный(по-умолчанию), ведется минимальный log об операциях в нотификаторе;
2. <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L12" target="_blank">Debug</a>], более детальный log, требуется только для анализа ошибок в работе нотификатора *(по-умолчанию False)*;
3. <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L13" target="_blank">exc_info</a>], полный Traceback ошибок *(по-умолчанию False)*;

## F.A.Q.
#### Оповещение не приходит в группу или в личку


## Последние значимые изменения

* Добавлены и изменены переменные в конфиг файле.
* Изменен XML.



---
<a id="note1" href="#note1ref"><sup>1</sup></a>Формирование списка urls в теле сообщения для быстрого перехода в разделы Zabbix (Trigger, History, Event, Acknowledget, Host)<br>
<a id="note2" href="#note2ref"><sup>2</sup></a> Формирование списка tags в теле сообщения для быстрого поиска событий в Telegram (Trigger Tags, Eventid, Itemid, Triggeid, Actionid)<br>
<a id="note3" href="#note3ref"><sup>3</sup></a> Кеш файл это json массив содержащий имена юзуров, групп, суппергруп и их идентификаторы(ИД). Безопасность Telegram не позволяет напрямую писать по имени, только по ИД. Чтобы получить данный ИД надо написать лично Вашему боту или бот должен быть добавлен в группу . Только после этого нотификатор "подключается" к боту и получает все обновления которые произошли у бота (getUpdates). Далее мы находим никнейм или имя групп, куда решили отправить нотификацию, и их ИД, которые и кладем в cash файл.
<a href="https://core.telegram.org/bots/faq#what-messages-will-my-bot-get" target="_blank">FAQ Telegram</a><br>
<a id="note4" href="#note4ref"><sup>4</sup></a> Управление через Trigger Tags (Не прикреплять график, не отправлять уведомление, без push в Telegram *dev* и т.п.)
