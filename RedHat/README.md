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

## Где размещать HTML-страницы
По умолчанию веб-контент размещается в каталоге:
```
/var/www/html
```
Замените или добавьте свои HTML-файлы в этот каталог, чтобы они были доступны по адресу вашего сервера.

## Рекомендации по конфигурации
- Основной конфигурационный файл: `/etc/httpd/conf/httpd.conf` (не рекомендуется изменять напрямую для пользовательских настроек).
- Для собственных настроек создайте отдельный файл, например:
```
vim /etc/httpd/conf.d/my_site.conf
```
Все файлы в `/etc/httpd/conf.d/` автоматически подключаются при запуске Apache. Это облегчает управление и обновление.

## Структура каталогов
- `/var/www/html` — основной каталог для размещения сайта
- `/etc/httpd/conf/httpd.conf` — основной конфиг
- `/etc/httpd/conf.d/` — дополнительные конфиги (рекомендуется для пользовательских настроек)

## Документация
- [Официальная документация Apache](https://httpd.apache.org/docs/)
