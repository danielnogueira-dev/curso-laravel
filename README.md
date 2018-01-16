# Curso de Laravel
## Faça um pull request e informe o que você deseja aprender no [Backlog.md](Backlog.md)

# Instalação no Ubuntu 16.04
## Instalação do PHP
```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php7.1-dev php7.1-cli php7.1-curl php7.1-mbstring php7.1-xml php7.1-sqlite3 php7.1-mysql php7.1-pgsql

```
## Instalação do XDebug
```
sudo apt-get install php-xdebug
```
## Configuração do XDebug
```
sudo vim /etc/php/7.1/cli/conf.d/20-xdebug.ini
```
```
zend_extension=xdebug.so
xdebug.remote_enable=1
xdebug.remote_handler=dbgp
xdebug.remote_mode=req
xdebug.remote_host=localhost
xdebug.remote_port=9000

;xdebug.remote_connect_back=1
;xdebug.remote_autostart=1
;xdebug.var_display_max_children=1024 
;xdebug.var_display_max_data=102400
;xdebug.var_display_max_depth=10
```
## Instalaçao da extensão (xdebug-helper) do Chrome
```
https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?utm_source=chrome-app-launcher-info-dialog
```
 ## Instalação do Composer
 ```
 php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
 ```

 ## Verificando instalação do composer
 ```
 composer --version
 ```

 ## Criando primeiro projeto em Laravel
 ```
 composer create-project --prefer-dist laravel/laravel nome_do_projeto
 cd nome_do_projeto
 php artisan serve
 ```

 # PHPStorm
 ## Instalando (Laravel Plugin)
 ```
 Abra o projeto no PHPStorm
 Menu "File" > "settings"
 Acesse "Editor" > "plugins"
 Clique no botão "Browse repositories"
 Pesquise por "Laravel Plugin"
 Clique em "Instalar"
 Reinicie o PHPStorm
 Para habilitar o Plugin, acesse o menu "File" > "settings"
 "Languages & Frameworks" > "PHP" > "Laravel"
 Deixe marcada as opções "Enable plugin for this project" e "Use AutoPopup for completion"
 ```
## Instalando o (laravel-ide-helper)
Referência: https://github.com/barryvdh/laravel-ide-helper
```
composer require --dev barryvdh/laravel-ide-helper
```

Adicione no arquivo "app/Providers/AppServiceProvider.php" no método de "register()"
```
public function register()
{
    if ($this->app->environment() !== 'production') {
        $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class);
    }
    // ...
}
```
Execute para criar o arquivo de configuração (config/ide-helper.php)
```
php artisan vendor:publish --provider="Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider" --tag=config
```

Instale o (doctrine/dbal) para auxiliar na geração da documentação para as Models
```
composer require doctrine/dbal
```

Execute para criar a documentação pra auxiliar a IDE
```
php artisan ide-helper:generate
php artisan ide-helper:meta
```
# Aula - Parte 1
## Configurando banco de dados (sqlite)
Edite o arquivo ".env", comente com "#" no início da linha as configurações do banco pro MySQL

```
#DB_CONNECTION=mysql
#DB_HOST=127.0.0.1
#DB_PORT=3306
#DB_DATABASE=homestead
#DB_USERNAME=homestead
#DB_PASSWORD=secret
```
Adicione a configuração para o (sqlite)
```
DB_CONNECTION=sqlite
```
Crie o arquivo "database/database.sqlite"
```
touch database/database.sqlite
```
Execute o comando para criar as tabelas no banco
```
php artisan migrate
```
## Criando um usuário de teste
```
php artisan tinker
```
```
factory(App\User::class)->create()
```

## Iniciando o servidor embutido do laravel
```
php artisan serve
```
Acesse no browser
http://localhost:8000/

## Criando uma rota de teste
Adicione no arquivo routes/api.php
```
Route::get('/users', function () {
    $users = App\User::all();
    return $users;
});
```
Acesse no browser
http://localhost:8000/api/users

## Instalaçao da extensão (JSONView) do Chrome
```
https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?utm_source=chrome-app-launcher-info-dialog
```

## Instalaçãi do (laravel-debugbar)
```
composer require barryvdh/laravel-debugbar --dev
```