#Cheat Sheet

```php
<?php //Todo código php começa com esta tag
//link: http://php.net/manual/pt_BR/language.oop5.interfaces.php
interface animal {
  public /*[public|protected|private]*/ function mover(/*[$a, $a='default']*/);
}
class mamiferos implements animal{
  private $especie = 'homo sapiens';
  const reino = 'animal';
  public function mover(){ return 'um passo'; }
  //métodos mágicos: http://php.net/manual/pt_BR/language.oop5.magic.php
  public function __construct(){ /*código de inicialização da classe*/}
  public function __get($name){ /*código que é executado quando se tenta acesso de leitura direto a um atributo não público*/}
  public function __set($name, $value) {/*identico ao anterior, só que para acesso de escrita*/}
  public function __toString(){/*método utilizado quando se tenta fazer uma conversão do objeto para texto*/
  	//constante mágica: http://php.net/manual/pt_BR/language.constants.predefined.php
  	return 'cachorro: ' . __LINE__; //concatenação de string 
  }
}
class cachorro extends mamiferos{
  public $idadeCanina;
  public static function getReino(){ return self::reino; }
}
echo  cachorro::getReino(); //utiliza método estático
$dog = new Cachorro(); //instanciação de classe simples
$m = 'mamiferos'; //atribuição de variável
$m = new $m(); //instanciação de classe através de variável //alteraçãod o tipo da variável m
var_dump(get_class($m)); //função que retorna nome da classe 
var_dump((string) $m) // conversão de objeto para string via __toString


#o código termina com a linha abaixo, sendo recomendado não usar o fechamento de tag quando se usa arquivo que contém PHP. Para evitar espaços em branco que podem forçar o iníco da sessão ao incluir tais arquivos.
?>
```
