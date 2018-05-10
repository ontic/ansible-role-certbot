# Documentation

## Example

```
certbot_install_from_source: yes
certbot_source_update: yes
certbot_source_path: '/opt/certbot'
certbot_source_repo: 'https://github.com/certbot/certbot.git'
certbot_source_version: 'master'
certbot_web_server_service_name: 'nginx'
certbot_auto_renew: yes
certbot_auto_renew_user: 'root'
certbot_auto_renew_hour: '2'
certbot_auto_renew_minute: '30'
certbot_certificates:
  - email: 'admin@company.com'
    webroot: '/var/www/html/letsencript'
    webroot_owner: 'web'
    domains:
      - 'company.com'
      - 'www.company.com'
      - 'blog.company.com'
      - 'www.blog.company.com'
```

## Role Variables

Available variables are listed below, along with default values (see [defaults/main.yml](/defaults/main.yml)):

```
certbot_install_from_source: no
```

Determines whether Certbot should be installed from source or package management, valid values are `yes` or `no`.

```
certbot_source_update: no
```

Whether an attempt is made to update Certbot when `certbot_install_from_source` is enabled, valid values are `yes` or `no`.

```
certbot_source_path: '/opt/certbot'
```

The directory path Certbot will be installed when `certbot_install_from_source` is enabled.


```
certbot_source_repo: 'https://github.com/certbot/certbot.git'
```

The Git repository Certbot will be cloned from when `certbot_install_from_source` is enabled.

```
certbot_source_version: 'master'
```

The Git repository branch/version to install Certbot from when `certbot_install_from_source` is enabled.

```
certbot_web_server_service_name: 'nginx'
```

The name of the daemon under which your web server runs. Typically this will be either `httpd`, `apache2` or `nginx`
which is the default. The service will be gracefully reloaded when a certificate is changed or automatically renewed.

```
certbot_auto_renew: yes
```

Whether a cron job should be created for automatically renewing certificates, valid values are `yes` or `no`.

```
certbot_auto_renew_hook: 'service {{ certbot_web_server_service_name }} reload'
```

The command invoked after a certificate is automatically renewed from a cron job.

```
certbot_auto_renew_user: '{{ ansible_user }}'
```

The user account in which cron jobs will run under when automatically renewing certificates.

```
certbot_auto_renew_hour: '2'
```

The hour when the renewal cron job should run.

```
certbot_auto_renew_minute: '30'
```

The minute when the renewal cron job should run.

```
certbot_certificates: []
```

A list of certificates to create and manage. Each certificate expects three parameters:

* `email` The email address used to agree to Let's Encrypt's TOS and subscribe to cert-related notifications.
* `webroot` The directory path Let's Encrypt's challenge files will be saved to.
* `webroot_owner` The user account who will take ownership of the webroot directory if needed to be created.
* `domains` A list of domains associated with the certificate, the first domain will be used as the certificate file name.
