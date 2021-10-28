Настраиваем логирование через Rsyslog. Vagrantfile поднимает две машины: web и log и проводит следующие манипуляции.

На машине web устанавливаются и запускаются nginx и rsyslog. Устанавливается audispd-plugins для удалённой отправки аудируемых событий. Настраиваем правило auditctl для nginx:# Сбор и анализ логов
Развёртывание центрального сервера для сбора логов

В Vagrant разворачиваем 2 машины web и log на web поднимаем nginx на log настраиваем центральный лог сервер:
journald
rsyslog
все критичные логи с web должны собираться и локально и удаленно все логи с nginx должны уходить на удаленный сервер (локально только критичные) логи аудита должны также уходить на удаленную систему.
## Выполнение практики
Настраиваем логирование через Rsyslog. 
Vagrantfile поднимает две машины web и log на машине web устанавливаются и запускаются nginx и rsyslog, устанавливается audispd-plugins для удалённой отправки аудируемых событий. Настраиваем правило auditctl для nginx:
````
sudo auditctl -w /etc/nginx/ -k nginx_watch
sudo auditctl -l >> /etc/audit/rules.d/nginx.rules
````
Правим конфигурацию nginx:
````
...
error_log syslog:server=192.168.11.151:514;
error_log /var/log/nginx/error.log;
...
access_log syslog:server=192.168.11.151:514 main;
...
````
Правим конфигурацию для отправки в rsyslog на машину log сообщений категорий: *.err, *.alert, *.crit, *.warning и *.notice. Правим конфигурацию audisp в /etc/audisp/plugins.d/au-remote.conf:
````
active = yes
direction = out
path = /sbin/audisp-remote
type = always
#args =
format = string
````
