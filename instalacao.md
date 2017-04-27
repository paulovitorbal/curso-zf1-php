# Instalação do PHP

Faça o download da versão desejada (arquivo zip) em: [windows.php.net](http://windows.php.net/download/);

Descompacte-o, sugiro escolher o endereço: ```c:\php```, aqui usaremos esse diretório como exemplo;

Adicione o diretório escolhido na variável ```PATH``` do windows.

Recomendo a instalação do [composer](https://getcomposer.org/doc/00-intro.md#installation-windows) como gerenciador de pacotes, siga as instruções do link;

## Conexão com o oracle;

Crie um arquivo com o código abaixo (no diretório de instalaçao) e execute para testar a conexão, lembre-se de alterar o tns, o nome de usuário e a senha;

```PHP
<?php
$tns = " 
(DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = yourip)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = orcl)
    )
  )
       ";
$db_username = "youname";
$db_password = "yourpassword";
try{
    $conn = new PDO("oci:dbname=".$tns,$db_username,$db_password);
}catch(PDOException $e){
    echo ($e->getMessage());
}
```

A saída do console deve ser semelhante a esta:
> $ php.exe oracle.php

> could not find driver
