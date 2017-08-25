# Setting up a local mirror for composer packages with Satis.
[![Build Status](https://travis-ci.org/midav/satis_server.svg?branch=master)](https://travis-ci.org/midav/satis_server)
=========

Solution will create a local mirror of a few packages to use it instead of the sources found on the Internet.

![Architecture](Architecture.png)

Requirements
------------

- Vagrant 1.8.1

Role Variables
--------------
Available variables are listed below, along with default values (see `defaults/main.yml`):

```
---

# System
satis_user: "satis"
satis_group: "satis"
satis_user_home: "/home/satis"

# Install
satis_installation: "{{ satis_user_home }}/satis"
satis_config_file: "{{ satis_user_home }}/satis.json"
satis_build_dir: "/opt/satis"

# Configuration
satis_repo_name: "Local Mirror for Composer Packages"
satis_repo_homepage: "http://localhost/"
satis_repos:
- type: "composer"
  url: "https://packagist.org"
satis_require: {}
satis_skip_dev: false
satis_composer_ignore_secure_http: false
satis_require_all: true
satis_require_dependencies: true
satis_require_dev_dependencies: false
satis_manage_cron: true
# PHP version

yum_php_version: "71w"

# Note: we need use 'apache' on Centos
php_owner: 'apache'
php_group: 'apache'

# PHP-FPM FastCGI
centos_php_fastcgi_listen: "/run/php-fpm/www.sock"
centos_nginx_fastcgi_server: "unix:{{ centos_php_fastcgi_listen }}"

# allow_url_fopen
#   Default Value: On
php_allow_url_fopen: "On"

php_disable_functions: "exec,passthru,shell_exec,system,proc_open,popen"
php_display_errors: "Off"
php_error_reporting: "E_ALL & ~E_DEPRECATED & ~E_STRICT"
php_memory_limit: "1024M"
php_opcache_enable: 1
php_opcache_revalidate_freq: 0
php_post_max_size: "20M"
php_serialize_precision: 17
php_session_cookie_httponly: 1
php_session_use_strict_mode: 1
php_soap_wsdl_cache_dir: '/php/cache/wsdl'
php_timezone: "Asia/Taipei"
php_upload_max_filesize: "20M"
php_upload_tmp_dir: "/php/cache/upload_tmp"

```

Dependencies
------------

- composer
- php
- nginx
- php-fpm
- centos 7

Example Playbook
----------------

How to use role:

    - hosts: servers
      roles:
         - { role: satis_server }

License
-------

MIT License (2015 - 2017). See the [LICENSE file](LICENSE) for details.

Author Information
------------------

- Twitter: [@vzakrinichniy](https://twitter.com/vzakrinichniy )