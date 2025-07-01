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

## Размещение сайта и настройка прав
1. Создайте каталог для сайта:
   ```bash
   mkdir /var/www/example
   chown -R $USER:$USER /var/www/example
   chmod -R 755 /var/www/example
   ```
2. Создайте файл index.html:
    
   В директории `Simple-HTML` этого репозитория находится пример файла `index.html`, который можно использовать для проверки работы. Просто скопируйте его содержимое в:
   ```bash
   vim /var/www/example/index.html
   ```
   
3. Измените права доступа:
   ```bash
   chown $USER:$USER /var/www/example/index.html
   chmod 644 /var/www/example/index.html
   ```

## Настройка виртуального хоста
1. Создайте новый конфиг:
   ```bash
   vim /etc/httpd/conf.d/example.conf
   ```
   Пример содержимого:
   ```apache
   <VirtualHost *:80>
       ServerAdmin webmaster@localhost
       ServerName example.com
       DocumentRoot /var/www/example
       <Directory "/var/www/example">
           AllowOverride All
       </Directory>
       ErrorLog /var/log/httpd/example_error.log
       CustomLog /var/log/httpd/example_access.log combined
   </VirtualHost>
   ```
2. Проверьте конфигурацию:
   ```bash
   apachectl configtest
   ```
   Должно быть: `Syntax OK`
3. Перезапустите Apache:
   ```bash
   systemctl restart httpd
   ```

## Проверка работы
Откройте IP-адрес сервера в браузере — должна открыться стартовая страница Apache.

## Структура каталогов
- `/var/www/html` — основной каталог для размещения сайта по умолчанию
- `/var/www/example` — каталог для вашего сайта
- `/etc/httpd/conf/httpd.conf` — основной конфиг
- `/etc/httpd/conf.d/` — рекомендуемое место для пользовательских конфигов (виртуальных хостов)

## Документация
- [Официальная документация Apache](https://httpd.apache.org/docs/)
