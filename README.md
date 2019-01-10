Software: PHP
=========

Установка PHP и PHP-FPM на сервер

Requirements
------------

* CentOS 7 на целевом хосте;
* Ansible 2.5 и выше.
* Загруженная роль установки NGINX;

Role Variables
--------------

### defaults/main.yml

#### /etc/php.ini

* **php\_php\_ini\_short\_open\_tag: "Off"** - указать значение для параметра short\_open\_tags в php.ini (доступные значения: On, Off);
* **php\_php\_ini\_post\_max\_size: "8M"** - значение параметра post_max_size в php.ini;
* **php\_php\_ini\_upload\_max\_filesize: "6M"** - значение параметра upload_max_filesize в php.ini;

#### /etc/php-fpm.d/www.conf

* **php\_php\_fpm\_port: 9005** - порт, на котором будет работать PHP-FPM.

### Other variables:
* **php\_version** - версия PHP, которая должна быть установлена (2 цифры без точки, например: 71);
* **php\_additional\_libs\_installed** - *список* дополнительных библиотек для PHP, которые установить для проекта;
* **php\_additional\_libs\_absent** - *список* дополнительных библиотек для PHP, которые требуется удалить с сервера.

Dependencies
------------

None

Example Playbook
----------------

```---
- name: Install NGINX
  hosts: all
  become: yes

  vars:
      nginx_repo_install: false

      php_version: 72
      php_additional_libs_installed:
          - php-pecl-memcache
          - php-pdo
          - php-mysqlnd
          - php-process
          - php-cli
          - php-mbstring
          - php-bcmath
          - php-pear
          - php-opcache

  roles:
      - software.nginx
      - software.php
```

Author Information
------------------

Cherniaev Y Aleksei cherniaev_a@tass.ru
