# <p align="center">Zabbix Notification with graph to Telegram
<p align="center">Нотификатор оповещений в Telegram для <a href="https://www.zabbix.com/documentation/7.0/en/manual"" >Zabbix 7</a>.<br>
Легкая установка, гибкая настройка, информативные сообщения.
<p align="center"><a href="https://www.zabbix.com/integrations/telegram#tab:3rd_party" target="_blank">Popular на www.zabbix.com</a> и <a href="https://share.zabbix.com/zabbix-tools-and-utilities/cat-notifications/zabbix-notification-telegram">share.zabbix.com</a>
<br>

## Возможности
- Графики, информативные заголовки, ссылки<a href="#note1" id="note1ref"><sup>1</sup></a>, тэги<a href="#note2" id="note2ref"><sup>2</sup></a> и упоминания объединены в **одно сообщение**.
- Формирование и обновление cash файла (privat, group, group -> supergroup)<a href="#note3" id="note3ref"><sup>3</sup></a>
- Гибкая настройка через конфигурационный файл, XML разметку в <a href="https://www.zabbix.com/documentation/current/manual/config/notifications/action" target="_blank">действиях триггеров</a> и Trigger Tags<a href="#note4" id="note4ref"><sup>4</sup></a>
- Маппинг Emoji статуса и важности события.
- Обьединение графиков в альбом.

## Логирование

Все основные события (отправка, добавления в cash файл, изменение группы в суппергруппу, ошибки, дебаг) логируются в файле ```znt.log```, Вы можете его найти по умолчанию ```/usr/lib/zabbix/alertscripts/zbxTelegram_files/znt.log``` (<a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L15" target="_blank">config_log_file</a>])
Поддерживаются три режима логирования:
1. Обычный(по-умолчанию), ведется минимальный log об операциях в нотификаторе;
2. <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L12" target="_blank">Debug</a>], более детальный log, требуется только для анализа ошибок в работе нотификатора *(по-умолчанию False)*;
3. <a href="https://github.com/xxsokolov/Zabbix-Notification-Telegram/blob/master/zbxTelegram_config.example.py#L13" target="_blank">exc_info</a>], полный Traceback ошибок *(по-умолчанию False)*;

