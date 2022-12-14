---
aliases: [ ]
created: 2022.09.28 10:07:14 вечера
modified: 2022.09.28 10:07:46 вечера
---
#🌐network

Настройка [[🌐telnet]] на [[📡 cisco]]

```Bash
# TELNET
enable # переход в привилегированный режим
configure terminal # переход в режим глобальной конфигурации. 
# В этом режиме возможен ввод команд, позволяющих конфигурировать общие характеристики системы
# Из режима глобальной конфигурации можно перейти во множество режимов конфигурации, специфических для конкретного протокола или функции.
username admin secret cisco # создаем пользователя с именем admin и паролем cisco.

# Настройка интерфейса - подключение по telnet
interface vlan 1 # переходим в виртуальный интерфейс и повесим на него IP-адрес. 
ip address 192.168.1.254 255.255.255.0 # присваиваем адрес 192.168.1.254 с маской 255.255.255.0
no shutdown # по умолчанию интерфейс выключен, поэтому включаем его
# В IOS 90% команд отменяются или выключаются путем приписывания перед командой «no».

line vty 0 15 # переходим в настройки виртуальных линий, где как раз живет Telnet. 
# От 0 до 15 означает, что применяем это для всех линий. 
# Всего можно установить на нем до 16 одновременных соединений.

transport input all # разрешаем соединение для всех протоколов. 

login local # указываем, что учетная запись локальная, и он будет проверять ее с той, что мы создали
copy running-config startup-config # обязательно сохраняем конфигурацию. Иначе после перезагрузки коммутатора все сбросится.
telnet 192.168.1.254       # подключиться по telnet
```
