# ilnurmn_infra
ilnurmn Infra repository

Домашнее задание к Лексии №5 
Знакомство с облачной инфраструкт фраструктурой Yandex.Cloud

Виртуальные машины:
  1
    Имя
      bastion
    Дата создания
      16 января 2022, в 16:44
    Внутренний FQDN
      bastion.ru-central1.internal
    Зона доступности
      ru-central1-a
    Ресурсы
    Платформа
      Intel Cascade Lake
    Гарантированная доля vCPU
      5%
    vCPU
      2
    RAM
      2 ГБ
    Объём дискового пространства
      13 ГБ
    Сеть
    Сетевой интерфейс
    Внутренний IPv4
      10.130.0.33
    Публичный IPv4
      51.250.12.59

  2
    Имя
      someinternalhost
    Дата создания
      16 января 2022, в 16:51
    Внутренний FQDN
      someinternalhost.ru-central1.internal
    Зона доступности
      ru-central1-a
    Ресурсы
    Платформа
      Intel Cascade Lake
    Гарантированная доля vCPU
      5%
    vCPU
      2
    RAM
      1 ГБ
    Объём дискового пространства
      13 ГБ
    Сеть
    Сетевой интерфейс
    Внутренний IPv4
      10.130.0.21


      
Задания

  1 Подключение через бастион хост выполнено (через VPN канал)
    adm00@ubuntu:~$ ssh -i ~/.ssh/appuser -A appuser@192.168.235.1
    appuser@bastion:~$ ssh 10.130.0.21
    appuser@someinternalhost:~$
  2 файл setupvpn.sh и cloud-bastion.ovpn в ветку репозитория cloud-bastion добавлены
  3 Опишите в README.md получившуюся конфигурацию
    bastion_IP = 51.250.12.59
    bastion_VPN_IP = 192.168.235.1
    bastion_Local_IP =10.130.0.33
    
    someinternalhost_IP = 10.130.0.21
    
    localhost_VPN_IP = 192.168.235.2
  4 "Labels" cloud-bastion к Pull Request добавлен

Самостоятельные задания:
  Подключения к someinternalhost в одну команду
    ssh -i ~/.ssh/appuser  -AJ appuser@51.250.12.59 appuser@10.130.0.21

  Дополнительное задание №1
    Вариант решения для подключения из консоли при помощи команды вида 
      ssh someinternalhost

        # На локальном хосте необходимо добавить в /etc/ssh/ssh_config следующие строки
        #
        Host bastion
             HostName 51.250.12.59
             User appuser
             Port 22
             Identityfile ~/.ssh/appuser
        Host someinternalhost
             HostName 10.130.0.21
             User appuser
             Port 22
             Identityfile ~/.ssh/appuser
             ProxyJump bastion
             ForwardAgent yes
        #
  Дополнительное задание №2
    С помощью сервисов sslip.io/xip.io и Lets Encript реализуйте использование валидного сертификата 
      https://51-250-12-59.sslip.io/login
	
	Сертификат
	Общее имя 51-250-12-59.sslip.io
	Страна US
	Организация Let's Encrypt
	Общее имя R3
	Действителен с Sun, 16 Jan 2022 17:25:51 GMT
	Действителен по Sat, 16 Apr 2022 17:25:50 GMT
	.............................................

