## Домашнее задание DNS

### Описание домашнего задания
```
1. Настроить master и slave сервера DNS
2. Настроить зоны DNS
●	web1 - смотрит на клиент1
●	web2 - смотрит на клиент2
3. Настроить split-dns
●	клиент1 - видит зоны dns.lab и newdns.lab , но в зоне dns.lab только web1
●	клиент2 видит только dns.lab

    VMs разворачивается в среде VMware vSphere 7 из шаблона Centos 7  

Файлы:

● newvms.yml:               ansible playbook развертывания VMs
● vars.yml:                 переменные для создания и наcтройки VMs
● host:                     inventory
● dns.yml:                  ansible playbook настройки серверов и клиентов DNS
● protocol.pdf:             проверка настрйки DNS
                            
● \templates\servers-resolv.conf.j2:
                            шаблон настройки /etc/resolv.conf серверов DNS
							
● \conf                     каталог файлов конфигурации и ключей
  ◦	client-motd:            файл, содержимое которого будет появляться перед пользователем,
                            который подключился по SSH
  ◦	client-resolv.conf:     /etc/resolv.conf клиентов, содержатся IP-адреса DNS-серверов
  ◦	servers-resolv.conf:    /etc/resolv.conf серверов DNS, содержатся IP-адреса DNS-серверов
  ◦	master-named.conf:      /etc/named.conf файл кофигурации master DNS
  ◦	slave-named.conf:       /etc/named.conf файл кофигурации slave DNS
  ◦	named.ddns.lab:         /etc/named/named.ddns.lab файл конфигурации зоны ddns.lab
  ◦	named.dns.lab:          /etc/named/named.dns.lab файл конфигурации зоны dns.lab
  ◦	named.dns.lab.client:   /etc/named/named.dns.lab.client файл конфигурации для view1 зоны ddns.lab
  ◦	named.dns.lab.rev:      /etc/named/named.dns.lab.rev файл конфигурации обратной зоны зоны dns.lab
  ◦	named.newdns.lab:       /etc/named/named.newdns.lab файл конфигурации зоны
  ◦	rndc.conf:              связь с сервером осуществляется с помощью цифровых подписей,
                            которые зависят от общего секрета,
                            обеспечить его можно только с помощью конфигурационного файла
  ◦	named.zonetransfer.key: /etc/named.zonetransfer.key ключ копирования зоны
