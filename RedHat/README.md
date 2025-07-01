# Apache HTTP Server на Red Hat

## Описание
Этот проект содержит инструкции по установке и базовой настройке веб-сервера Apache на дистрибутивах Red Hat (RHEL, CentOS, Almalinux).

## Установка
```bash
dnf -y update && dnf -y install httpd
```

## Запуск и автозагрузка
```bash
systemctl start httpd && systemctl enable httpd
```

## Проверка статуса
```bash
systemctl status httpd
```

## Настройка фаервола
На Red Hat после установки нужно разрешить HTTP/HTTPS в фаерволе:
```bash
firewall-cmd --permanent --add-service=http --add-service=https
firewall-cmd --reload && firewall-cmd --list-all
```
В блоке Services должны отображаться http и https.

## Проверка работы
Откройте IP-адрес сервера в браузере — должна открыться стартовая страница Apache.

## Расширенные настройки
Основной конфигурационный файл:
```bash
vim /etc/httpd/conf/httpd.conf
```

## Документация
- [Официальная документация Apache](https://httpd.apache.org/docs/)
