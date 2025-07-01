# Apache + PHP на Ubuntu

## Установка PHP
```bash
apt update && apt -y install php libapache2-mod-php
```

## Проверка установки
```bash
php -v
```

## Настройка Apache для работы с PHP
Модуль `libapache2-mod-php` обычно активируется автоматически. Если нет — активируйте вручную:
```bash
a2enmod php8.1
systemctl restart apache2
```

## Настройка приоритета индекса
Создайте или отредактируйте файл `.htaccess` в каталоге сайта:
```bash
vim /var/www/example/.htaccess
```
Добавьте строку:
```
DirectoryIndex index.php index.html
```

## Создание тестового PHP-файла
```bash
vim /var/www/example/index.php
```
Пример содержимого:
```php
<?php phpinfo();
```

## Проверка работы
Откройте в браузере: `http://<ваш_сервер>/` — должна появиться страница с информацией о PHP.

## Рекомендации по безопасности
- Не оставляйте phpinfo() на рабочем сервере. Используйте только для теста.

## Документация
- [PHP для Apache (официально)](https://www.php.net/manual/ru/install.unix.apache2.php)




