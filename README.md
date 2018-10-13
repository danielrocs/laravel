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

### Etapa 1: Instale o Apache:

Passo 1: Instale o servidor Web Apache2, curl e o pacote git

```bash
$ sudo apt update
$ sudo apt install apache2
$ sudo apt install git
$ sudo apt install curl
```

Comando usados para stop, start e enable Apache2 `services` 

```bash
$ sudo systemctl stop apache2.service
$ sudo systemctl start apache2.service
$ sudo systemctl enable apache2.service
```

### Etapa 2: Instale o PHP 7.2 e seus módulos

Para instalar o PHP e os módulos relacionados, execute os comandos abaixo
```bash
$ sudo apt install php7.2 libapache2-mod-php7.2 php7.2-mbstring php7.2-xmlrpc php7.2-soap php7.2-gd php7.2-xml php7.2-cli php7.2-zip
```

Depois de instalar o PHP, execute os comandos abaixo para abrir o arquivo padrão do PHP-FPM.
```bash
$ sudo nano /etc/php/7.2/apache2/php.ini
```

Em seguida, faça a alteração das seguintes linhas abaixo no arquivo e salve.

- memory_limit = 256M
- upload_max_filesize = 64M
- cgi.fix_pathinfo=0  *não fazer alteração
- max_input_time = 60 *Em segundos
- post_max_size = 80M

Instale o PHP Extension para suporte ao MySQL:
```bash
$ sudo apt install php-mysql -y
```

#### Instalar módulos do PHP 7

Você também pode precisar instalar módulos com base nos requisitos de sua aplicação. Use o seguinte comando para procurar os módulos do PHP 7 disponíveis no repositório de pacotes.
```bash
$ sudo apt-cache search php7*
```

### Etapa 3: Instalar o Composer para fazer o download do Laravel

Execute os comandos abaixo para instalar o pacote composer e instale, você deve ter o pacote curl instalado para os comandos funcionarem.
```bash
$ curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

#### Iniciando um Projeto
Para iniciar um projeto mude para o diretório wwww e execute os comandos abaixo para fazer o download e instalar o Laravel para o projeto que você deseja criar ... nomeie o projeto como você quiser ... exemplo chamando de "MyProject".
```bash
$ cd /var/www/html
$ sudo composer create-project laravel/laravel MyProject
```

Depois de executar os comandos acima, um novo diretório de projeto será criado. Execute os comandos abaixo para definir as permissões corretas para esse diretório.
```bash
$ sudo chown -R www-data:www-data /var/www/html/MyProject/
$ sudo chmod -R 755 /var/www/html/MyProject/
```

### Etapa 4: Configure Apache2
Finalmente, configure o arquivo de configuração do site Apahce2 para o Laravel. Este arquivo controlará como os usuários acessam o conteúdo do Laravel. Execute os comandos abaixo para criar um novo arquivo de configuração chamado laravel.conf
```bash
$ sudo nano /etc/apache2/sites-available/laravel.conf
```
Em seguida, copie e cole o conteúdo abaixo no arquivo e salve-o. Substitua a linha realçada pelo seu próprio nome de domínio e localização da raiz do diretório.
```bash
<VirtualHost *:80>   
  ServerAdmin admin@example.com
     DocumentRoot /var/www/html/MyProject/public
     ServerName example.com

     <Directory /var/www/html/MyProject/public>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Salve o arquivo e saia.

Dica: Para remover um diretório 
```bash
$ sudo rm -Rf MyProject
```

Outra configuração mais simples
```bash
<VirtualHost *:80>
    ServerName yourdomain.tld

    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/your-project/public

    <Directory /var/www/html/your-project>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Passo 5: Ative o Laravel e o Rewrite Module

Depois de configurar o VirtualHost acima, habilite-o executando os comandos abaixo
```bash
$ sudo a2dissite 000-default.conf
$ sudo a2ensite laravel.conf
$ sudo a2enmod rewrite
```

### Etapa 6: Reinicie o Apache2

Para carregar todas as configurações acima, reinicie o Apache2 executando os comandos abaixo.
```bash
$ sudo systemctl restart apache2.service
```

#### Configurações do Apache

Se você puder ler esta página, isso significa que o servidor HTTP Apache instalado neste site está funcionando corretamente. Você deve substituir esse arquivo (localizado em /var/www/html/index.html) antes de continuar a operar seu servidor HTTP.

A configuração padrão do Apache2 do Ubuntu é diferente da configuração padrão do upstream e é dividida em vários arquivos otimizados para interação com as ferramentas do Ubuntu. O sistema de configuração está totalmente documentado em /usr/share/doc/apache2/README.Debian.gz. Consulte isto para a documentação completa. A documentação do próprio servidor da web pode ser encontrada acessando o manual se o pacote apache2-doc foi instalado neste servidor.

O layout de configuração para uma instalação do servidor da web Apache2 em sistemas Ubuntu é o seguinte:
```bash
/etc/apache2/
|-- apache2.conf
|       `--  ports.conf
|-- mods-enabled
|       |-- *.load
|       `-- *.conf
|-- conf-enabled
|       `-- *.conf
|-- sites-enabled
|       `-- *.conf
```
O apache2.conf é o arquivo de configuração principal. Ele coloca as peças juntas, incluindo todos os arquivos de configuração restantes ao inicializar o servidor da web.

O ports.conf é sempre incluído no arquivo de configuração principal. Ele é usado para determinar as portas de escuta para conexões de entrada e esse arquivo pode ser personalizado a qualquer momento.

Os arquivos de configuração nos diretórios mods-enabled/, conf-enabled/ e sites-enabled/ contêm contêineres de configuração específicos que gerenciam módulos, fragmentos de configuração global ou configurações de host virtual, respectivamente.

Eles são ativados por symlinking arquivos de configuração disponíveis de seus respectivos * -available/ contrapartes. Estes devem ser gerenciados usando nossos ajudantes a2enmod, a2dismod, a2ensite, a2dissite e a2enconf, a2disconf. Veja suas respectivas páginas de manual para informações detalhadas.

O binário é chamado apache2. Devido ao uso de variáveis de ambiente, na configuração padrão, o apache2 precisa ser iniciado interrompido com /etc/init.d/apache2 ou apache2ctl. Chamar /usr/bin/apache2 diretamente não funcionará com a configuração padrão.

Observações: Por padrão, o Ubuntu não permite acesso através do navegador da web a qualquer arquivo, exceto aqueles localizados em /var/www, public_html (quando habilitado) e  /usr/share (para aplicativos da web). Se o seu site estiver usando uma raiz de documento da Web localizada em outro lugar (como em /srv), talvez você precise incluir na lista de permissões o diretório raiz do documento em /etc/apache2/apache2.conf.

A raiz do documento padrão do Ubuntu é /var/www/html. Você pode criar seus próprios hosts virtuais em /var/www. Isso é diferente dos lançamentos anteriores, o que proporciona maior segurança na caixa.

Em caso de erro na exibição atualize o arquivo `apache2.conf`
```bash
$ sudo nano /etc/apache2/apache2.conf
```

```bash
Atualize o arquivo para 
<Directory /var/www/html/MyProject/public>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
</Directory>
```

#### Outras configurações do Apache
Para habilitar ou desabilitar um site hospedado com o Apache, você pode usar os comandos 'a2ensite' e 'a2dissite', respectivamente. Ambos os comandos usam essencialmente a mesma sintaxe:

- a2ensite <site>
- a2dissite <site>

onde '<site>' é o nome do arquivo de configuração do Host Virtual do seu site, localizado em '/ etc / apache2 / sites-available /', menos a extensão '.conf'. Por exemplo, se o arquivo de configuração do Host Virtual do seu site se chamar 'example.com.conf', então os comandos se parecerão com </ site>
```bash
$ a2ensite example.com
$ a2dissite example.com
```

Existem outras maneiras mais complicadas de fazer isso, mas esses comandos basicamente apenas automatizam esses processos, então meu conselho é usar esses comandos para garantir que tudo esteja sempre configurado corretamente. Além disso, lembre-se de reiniciar o Apache depois de executar esses comandos. O comando exato dependerá de qual distribuição Linux você está usando, mas provavelmente será um dos dois comandos a seguir:
```bash
$ sudo systemctl restart apache2
$ sudo service apache2 restart
```


#### Ajustar o Firewall para Permitir Tráfego Web
Agora, assumindo que você seguiu as instruções de configuração inicial do servidor para habilitar o firewall UFW, certifique-se de que seu firewall permite tráfego HTTP e HTTPS. Você pode certificar-se de que o UFW tem um perfil de aplicativo para o Apache assim:
```bash
$ sudo ufw app list
```

Se você olhar para o perfil Apache Full, ele deve mostrar que ele habilita tráfego para as portas 80 e 443:
```bash
$ sudo ufw app info "Apache Full"
```

Permita o tráfego entrante HTTP e HTTPS para esse perfil:
```bash
$ sudo ufw allow in "Apache Full"
```

Você pode fazer uma verificação imediata para verificar se tudo correu como planejado visitando o endereço IP público do seu servidor no seu navegador web (Veja a nota abaixo do próximo cabeçalho para descobrir qual é o seu endereço IP público se você ainda não tiver essa informação)
```bash
$ http://ip_do_seu_servidor
```

Antes de implementarmos as alterações que fizemos, verifique para ter certeza de que não cometemos nenhum erro de sintaxe:
```bash
$ sudo apache2ctl configtest
```

### Etapa 6 - Instalação do MySQL
Agora que temos nosso servidor web pronto e funcionando, é hora de instalar o MySQL.
```bash
$ sudo apt install mysql-server
```

#### Teste o MySql
Acesse o MySQL’s SQL pelo shell:
```bash
$ sudo mysql -u root -p
```

Crie um banco de dados e um usuário com permissões para isso. Neste exemplo, o banco de dados é chamado de webdata, o usuário webuser e senha password. Certifique-se de digitar sua própria senha. Isso deve ser diferente da senha raiz do MySQL:
```bash
CREATE DATABASE webdata;
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;

GRANT ALL ON webdata.* TO 'webuser' IDENTIFIED BY 'password';
GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' IDENTIFIED BY 'password';

FLUSH PRIVILEGES;
EXIT;
```


Quando a instalação estiver concluída, execute um script de segurança simples que vem pré-instalado com o MySQL e que irá remover alguns padrões perigosos e bloquear o acesso ao seu sistema de banco de dados. Inicie o script interativo executando:
```bash
$ sudo mysql_secure_installation
```
Você será perguntado se você quer configurar o VALIDATE PASSWORD PLUGIN.

Nota: A habilitação dessa funcionalidade é algo que deve ser avaliado. Se habilitado, senhas que não seguem o critério especificado serão rejeitadas pelo MySQL com um erro. Isso irá causar problemas se você utilizar uma senha fraca juntamente com software que configura automaticamente as credenciais de usuário do MySQL, tais como os pacotes do Ubuntu para o phpMyAdmin. É seguro deixar a validação desativada, mas você deve sempre utilizar senhas fortes e exclusivas para as credenciais do banco de dados.

Responda Y para Sim, ou qualquer outra coisa para continuar sem a habilitação.

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:

Se você responder "yes", você será solicitado a selecionar um nível de validação de senha. Tenha em mente que se você digitar 2, para o nível mais forte, você receberá erros quando tentar configurar qualquer senha que não contenha números, letras maiúsculas e minúsculas, e caracteres especiais, ou que seja baseada em palavras comuns do dicionário.

There are three levels of password validation policy:

- LOW    Length >= 8
- MEDIUM Length >= 8, numeric, mixed case, and special characters
- RONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1

Independentemente de você escolher configurar o VALIDATE PASSWORD PLUGIN, seu servidor em seguida irá solicitar que você selecione e confirme a senha para o usuário root do MySQL. Esta é uma conta administrativa no MySQL que possui privilégios avançados. Pense nela como sendo similar à conta de root para o próprio servidor (embora esta que você está configurando agora é uma conta específica do MySQL). Certifique-se de que esta é uma senha forte e exclusiva, e não a deixe em branco.

Se você habilitou a validação de senha, será mostrado a força da senha de root atual, e será perguntado se você quer alterar aquela senha. Se você estiver satisfeito com sua senha atual, digite N para "não" no prompt:

Using existing password for root.

Estimated strength of the password: 100

Change the password for root ? ((Press y|Y for Yes, any other key for No) : n

Para o restante das perguntas, pressione Y e aperte a tecla Enter para cada prompt. Isso irá remover alguns usuários anônimos e o banco de dados de teste, desabilitar logins remotos de root, e carregar essas novas regras de forma que o MySQL respeite imediatamente as alterações que fizemos. 

#### 

Estas etapas funcionaram para mim em vários sistemas usando Ubuntu 16.04, Apache 2.4, MariaDB, PDO

    log into MYSQL as root

    mysql -u root

    Grant privileges. To a new user execute:

    CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost';
    FLUSH PRIVILEGES;

    bind to all addresses:

The easiest way is to comment out the line in your /etc/mysql/mariadb.conf.d/50-server.cnf or /etc/mysql/mysql.conf.d/mysqld.cnf file, depending on what system you are running:

    #bind-address = 127.0.0.1 

    exit mysql and restart mysql

    exit
    service mysql restart

By default it binds only to localhost, but if you comment the line it binds to all interfaces it finds. Commenting out the line is equivalent to bind-address=*.

To check the binding of mysql service execute as root:

    netstat -tupan | grep mysql


