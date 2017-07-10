# Instalação do PHP

Faça o download da versão desejada (arquivo zip) em: [windows.php.net](http://windows.php.net/download/);

Descompacte-o, sugiro escolher o endereço: ```c:\php```, aqui usaremos esse diretório como exemplo;

Adicione o diretório escolhido na variável ```PATH``` do windows.

Renomeie o arquivo ```php.ini-development``` para ```php.ini```;

Recomendo a instalação do [composer](https://getcomposer.org/doc/00-intro.md#installation-windows) como gerenciador de pacotes, siga as instruções do link;

## Conexão com o oracle;

Crie um arquivo com o código abaixo (no diretório de instalaçao) e execute para testar a conexão, lembre-se de alterar o tns, o nome de usuário e a senha;

```PHP
<?php
$tns = " (DESCRIPTION = (ADDRESS_LIST= (LOAD_BALANCE=on)(FAILOVER=ON) (ADDRESS=(PROTOCOL=tcp)(HOST=host.rede)(PORT=1521)) ) (CONNECT_DATA = (SERVICE_NAME = service_name) (SERVER = DEDICATED) ) )";
$db_username = "user";
$db_password = "pass";

$conn = $conn = oci_connect($db_username, $db_password, $tns);
$stid = oci_parse($conn, 'SELECT sysdate FROM dual');
oci_execute($stid);
$nrows = oci_fetch_all($stid, $res);
var_dump($res);

```

A saída do console deve ser semelhante a esta:
>php.exe oracle.php
> 
> PHP Fatal error:  Call to undefined function oci_connect() in C:\php\oracle.php on line 7
> 
> Fatal error: Call to undefined function oci_connect() in C:\php\oracle.php on line 7


Isso significa que o driver não está habilitado;

Altere o arquivo ```php.ini``` retirando os comentários das seguintes linhas;

De:
```
;;;;;;;;;;;;;;;;;;;;;;
; Dynamic Extensions ;
;;;;;;;;;;;;;;;;;;;;;;
;...
;... várias extensões aqui
;...
;extension=php_oci8_12c.dll  ;
```

Para:

```
extension=php_oci8_12c.dll;
```


Ao executar novamente o resultado esperado é algo semelhante a:
```PHP
$ php.exe oracle.php                 
array(1) {                           
  ["SYSDATE"]=>                      
  array(1) {                         
    [0]=>                            
    string(8) "27/04/17"             
  }                                  
}                                    
```

Para utilizar o PHP7, recomendo o seguinte pacote de instalação: [PHP 7.1.7 NTS x64](http://windows.php.net/downloads/releases/php-7.1.7-nts-Win32-VC14-x64.zip)

Com a seguinte biblioteca OCI8: [OCI8-2.1.3 NTS VC14 x64](http://windows.php.net/downloads/pecl/releases/oci8/2.1.3/php_oci8-2.1.3-7.1-nts-vc14-x64.zip)

## Inciciando um servidor web (built in server)

Use o comando abaixo:
```
php -S localhost:80 -t public
```
O argumento ```-S localhost:80``` explicita qual o endereço e a porta que o servidor web responderá, poderia se colocar por exemplo um endereço ```acme.com:8080```;

O argumento ```-t public``` indica em qual diretório o servidor irá utilizar como raíz, no caso ele irá procurar por um diretório ```public``` dentro do diretório atual;

