Download Wamp Server
https://sourceforge.net/projects/wampserver/files/latest/download

"Git for windows" no site "https://gitforwindows.org"
"https://getcomposer.org/download/" no site " Composer" durante instalação setar PHP 7.x do

É necessário usar o composer 1.9.3 https://getcomposer.org/download/1.9.3/composer.phar 
substitua o arquivo nas pastas C:\composer e C:\ProgramData\ComposerSetup\bin

Criar usuário e banco de dados

CREATE USER 'novosga2'@'localhost' IDENTIFIED BY '150769';
GRANT ALL PRIVILEGES ON novosga2.* TO 'novosga'@'localhost' IDENTIFIED BY '150769';
FLUSH PRIVILEGES;

Abra o GitBash, acesse a pasta do Wamp www digite os comandos abaixo

composer create-project "novosga/novosga:^2.0" novosga2

Se apresentar o erro " [ErrorException]
  curl_multi_setopt(): CURLPIPE_HTTP1 is no longer supported"
  
Localize o arquivo php.ini e edite a linha memory_limit e set o valor com -1
depois digite o comando 

composer update -v symfony/flex

Ativação do serviço NovoSGA

export APP_ENV=prod
export LANGUAGE=pt_BR
export DATABASE_URL="mysql://novosga:150769@127.0.0.1:3306/novosga2?charset=utf8mb4&serverVersion=5.7"

bin/console novosga:install


Na pasta /novosga2/public usando GitBash

$ echo 'Options -MultiViews
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule (.*)$ index.php [QSA,L]
SetEnv APP_ENV prod
SetEnv LANGUAGE pt_BR
SetEnv DATABASE_URL mysql://novosga:150769@127.0.0.1:3306/novosga2?charset=utf8mb4&serverVersion=5.7
' > ./.htaccess


