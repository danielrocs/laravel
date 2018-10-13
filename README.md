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

#### Instalar módulos do PHP 7

Você também pode precisar instalar módulos com base nos requisitos de sua aplicação. Use o seguinte comando para procurar os módulos do PHP 7 disponíveis no repositório de pacotes.
```bash
$ sudo apt-cache search php7*
```

