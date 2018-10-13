# Laravel
Laravel - Exemplo e aplicações de teste

### Atualizar o composer

Verifica a vesão do Composer
```sh
$ composer -V
```
Atualizar o [Composer](https://getcomposer.org/download/)

### Update Via Laravel Installer

Primeiramente, download the last version of Laravel installer using Composer:
```sh
$ composer global require "laravel/installer"
```

### Criar um projeto em Laravel

Primeiramente, download the last version of Laravel installer using Composer:
```sh
$ laravel new CebTecHost
```

Displaying Your Current Laravel Version

You may also view the current version of your Laravel installation using the --version option:
```sh
$ php artisan --version
```

### Testando a aplicação

```sh
$ php artisan serve
```

## Prerequisites
<ul>
<li>After cloning this repository, go to the root folder, run the following command/s,
<pre>
    composer install
    composer update</pre>
</li>
<li>Rename .env.example to .env and provide your database details there.</li>
<li>Run <code>php artisan migrate</code> to create database table.</li>
<li>Run <code>php artisan key:generate</code> to set application key. </li>

</ul>

## Instalar Laravel no Ubuntu 18.04

### Instale o Apache:

Passo 1: Instale o servidor Web Apache2

```bash
$ sudo apt update
$ sudo apt install apache2
```

Comando usados para stop, start e enable Apache2 `services` 

```bash
$ sudo systemctl stop apache2.service
$ sudo systemctl start apache2.service
$ sudo systemctl enable apache2.service
```

### Step 2: Install PHP 7.2 and Related Modules

Para instalar o PHP e os módulos relacionados, execute os comandos abaixo
```bash
$ sudo apt install php7.2 libapache2-mod-php7.2 php7.2-mbstring php7.2-xmlrpc php7.2-soap php7.2-gd php7.2-xml php7.2-cli php7.2-zip
```

Depois de instalar o PHP, execute os comandos abaixo para abrir o arquivo padrão do PHP-FPM.
```bash
$ sudo nano /etc/php/7.2/apache2/php.ini
```

Em seguida, faça a alteração das seguintes linhas abaixo no arquivo e salve.

memory_limit = 256M
upload_max_filesize = 64M
cgi.fix_pathinfo=0



