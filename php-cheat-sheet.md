# Cheat Sheet
## Exemplo 1
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
//traits: http://php.net/manual/pt_BR/language.oop5.traits.php
trait latir{
	public function latirAlto(int $qtd = 5){ //type hint: http://php.net/manual/pt_BR/functions.arguments.php#functions.arguments.type-declaration
		echo "au au au({$qtd}x)\n";
	}
	public function latirTextao($qtd = 5){
		echo <<<TEXTAO
bá ´blá blá 
bla bla bla
qtd: $qtd \n
TEXTAO;
	}
	public function latirLiteralmente($qtd=5){
		echo 'au au au ({$qtd}x)\n';
	}
}
class cachorro extends mamiferos{
	use latir;
  	public $idadeCanina;
  	public static function getReino(){ return self::reino; }
}
echo  cachorro::getReino(); //utiliza método estático
$dog = new Cachorro(); //instanciação de classe simples
$m = 'mamiferos'; //atribuição de variável
$m = new $m(); //instanciação de classe através de variável //alteraçãod o tipo da variável m
var_dump(get_class($m)); //função que retorna nome da classe //função de debug
var_dump((string) $m); // conversão de objeto para string via __toString
$dog->latirAlto();
$dog->latirTextao();
$dog->latirLiteralmente();

#o código termina com a linha abaixo, sendo recomendado não usar o fechamento de tag quando se usa arquivo que contém PHP. Para evitar espaços em branco que podem forçar o iníco da sessão ao incluir tais arquivos.
?>
```
## Exemplo 2

[Autoload de classes](http://php.net/manual/pt_BR/language.oop5.autoload.php)
```php
<?php
spl_autoload_register(function ($class_name) {
    include $class_name . '.php';
});
$obj  = new MyClass1(); //auto inclui as classes MyClass1 do arquivo MyClass1.php sob demanda
$obj2 = new MyClass2(); //auto inclui as classes MyClass2 do arquivo MyClass2.php sob demanda
```
