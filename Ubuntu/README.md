# Apache HTTP Server на Ubuntu

## Описание
Этот проект содержит инструкции по установке и базовой настройке веб-сервера Apache на дистрибутивах Ubuntu (и производных).

## Установка
```bash
apt update && apt install -y apache2
```

## Запуск и автозагрузка
```bash
systemctl start apache2 && systemctl enable apache2
```

## Проверка статуса
```bash
systemctl status apache2
```

## Настройка фаервола
На Ubuntu после установки нужно разрешить HTTP/HTTPS в фаерволе:
```bash
ufw allow 'Apache Full'
ufw reload
ufw status numbered
```

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
   vim /etc/apache2/sites-available/example.conf
   ```
   Пример содержимого:
   ```apache
   <VirtualHost *:80>
       ServerAdmin test@yandex.ru
       ServerName example.com
       DocumentRoot /var/www/example
       <Directory "/var/www/example">
           AllowOverride All
       </Directory>
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```
2. Включите сайт и отключите сайт по умолчанию:
   ```bash
   a2ensite example.conf
   a2dissite 000-default.conf
   ```
3. Проверьте конфигурацию:
   ```bash
   apache2ctl configtest
   ```
   Должно быть: `Syntax OK`
4. Перезапустите Apache:
   ```bash
   systemctl restart apache2
   ```

## Проверка работы
Откройте IP-адрес сервера в браузере — должна открыться стартовая страница Apache.

## Структура каталогов
- `/var/www/html` — основной каталог для размещения сайта по умолчанию
- `/var/www/example` — каталог для вашего сайта
- `/etc/apache2/apache2.conf` — основной конфиг
- `/etc/apache2/sites-available/` — рекомендуемое место для пользовательских конфигов (виртуальных хостов)
- `/etc/apache2/sites-enabled/` — активированные конфиги

## Документация
- [Официальная документация Apache](https://httpd.apache.org/docs/)
