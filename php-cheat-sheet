#Cheat Sheet

```php
<?php //Todo código php começa com esta tag e termina com ?>, sendo este opcional quando se trata de arquivo puramente php
//link: http://php.net/manual/pt_BR/language.oop5.interfaces.php
interface animal {
  [public|protected|private] function mover([$a, $a='default']);
}
class mamiferos implements animal{
  private $especie = 'homo sapiens';
  const reino = 'animal';
  public function mover(){ return 'um passo'; }
}
class cachorro extends mamiferos{
  public $idadeCanina;
  http://php.net/manual/pt_BR/language.oop5.magic.php
  public function __construct(){ /*código de inicialização da classe*/}
  public function __get($name){ /*código que é executado quando se tenta acesso de leitura direto a um atributo não público*/}
  public function __set($name, $value) {/*identico ao anterior, só que para acesso de escrita*/}
  public function __toString(){/*método utilizado quando se tenta fazer uma conversão do objeto para texto*/}
  public function getReino(){ return self::reino; }
}
```
