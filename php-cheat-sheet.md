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
[Funções anonimas](http://php.net/manual/pt_BR/functions.anonymous.php)
```php
<?php
spl_autoload_register(function ($class_name) {
    include $class_name . '.php';
});
$obj  = new MyClass1(); //auto inclui as classes MyClass1 do arquivo MyClass1.php sob demanda
$obj2 = new MyClass2(); //auto inclui as classes MyClass2 do arquivo MyClass2.php sob demanda
```

## Tipos de variáveis
* boolean, pode assumir os valores TRUE ou FALSE;
* integer, números inteiros incluindo representações binárias, hexadeciamais e octais;
* float, números de ponto flutuante
```php
<?php
$a = 1.234; 
$b = 1.2e3; 
$c = 7E-10;
?>
```
* string, cadeia de caracteres;
* array, mapeamento de valores e chaves. Pode ter como chave valores inteiros, ou strings.
```php
<?php
$array = [ //php 5.4
    "foo" => "bar",
    "bar" => "foo",
];
$array = array(
    "foo" => "bar",
    "bar" => "foo",
    100   => -100,
    -100  => 100,
);
var_dump($array);
var_dump($array['foo']);
var_dump($array[-100]);

<?php
function getArray() {
    return array(1, 2, 3);
}
$secondElement = getArray()[1]; //deferência //PHP 5.4
// PHP 5.3
$tmp = getArray();
$secondElement = $tmp[1];

$array[] = 'novo elemento no final do array';
```
* objetos, são instâncias de classes;
* resources, tipo especial de variável que representa um recurso do sistema operacional, como uma conexão de banco, ou um arquivo aberto;
* NULL, valor nulo, ocorre quando:
  * foi explicitamente utilizado a constante NULL em uma atribuição;
  * não foi setado nenhum valor até o momento;
  * foi utilizado a função unset();
* variavéis pré definidas, setadas pelo servidor de aplicação:
  * $_SERVER;
  * $_POST;
  * $_GET;
  * $_ENV;
  * $_REQUEST;
  * $_COOKIE;
  * $_FILES;
  * $_GLOBALS;

## Operadores
* Matemáticos:
```php
<?php
+$a; //identidade (conversão para int ou float, o que for apropriado);
-$a; //negação (o valor negativo de $a);
$a % $b; //módulo (resto da divisão inteira);
$a ** $b; //exponênciação (a elevado a b); PHP 5.6
```
* Operadores bit-a-bit (bitwise)

| Exemplo 	| Nome 	| Resultado 	|
|------------------------------	|-------------------------	|----------------------------------------------------------------------------------------------	|
| $a & $b 	| E (AND) 	| Os bits que estão ativos tanto em $a quanto em $b são ativados. 	|
| $a | $b 	| OU (OR inclusivo) 	| Os bits que estão ativos em $a ou em $b são ativados. 	|
| $a ^ $b 	| XOR (OR exclusivo) 	| Os bits que estão ativos em $a ou em $b, mas não em ambos, são ativados. 	|
| ~ $a 	| NÃO (NOT) 	| Os bits que estão ativos em $a não são ativados, e vice-versa. 	|
| $a << $b 	| Deslocamento à esquerda 	| Desloca os bits de $a $b passos para a esquerda (cada passo significa "multiplica por dois") 	|
| $a >> $b 	| Deslocamento à direita 	| Desloca os bits de $a $b passos para a direita (cada passo significa "divide por dois") 	|

* Operadores de comparação

| Exemplo   | Nome                      | Resultado                                                                                                                                       |
|-----------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| $a == $b  | Igual                     | Verdadeiro (TRUE) se $a é igual a $b.                                                                                                           |
| $a === $b | Idêntico                  | Verdadeiro (TRUE) se $a é igual a $b, e eles são do mesmo tipo.                                                                                 |
| $a != $b  | Diferente                 | Verdadeiro se $a não é igual a $b.                                                                                                              |
| $a <> $b  | Diferente                 | Verdadeiro se $a não é igual a $b.                                                                                                              |
| $a !== $b | Não idêntico              | Verdadeiro de $a não é igual a $b, ou eles não são do mesmo tipo (introduzido no PHP4).                                                         |
| $a < $b   | Menor que                 | Verdadeiro se $a é estritamente menor que $b.                                                                                                   |
| $a > $b   | Maior que                 | Verdadeiro se $a é estritamente maior que $b.                                                                                                   |
| $a <= $b  | Menor ou igual            | Verdadeiro se $a é menor ou igual a $b.                                                                                                         |
| $a >= $b  | Maior ou igual            | Verdadeiro se $a é maior ou igual a $b.                                                                                                         |
| $a <=> $b | Spaceship (nave espacial) | Um integer menor que, igual a ou maior que zero quando $a é, respectivamente, menor que, igual a ou maior que $b. Disponível a partir do PHP 7. |

*Operador de controle de erro

\@ quando precede uma empressão em PHP, qualquer mensagem de erro que possa ser gerada por aquela expressão será ignorada;
**:no_entry_sign:NÃO USE ISSO!**

*Operador de execução
\`\` acento grave, o PHP tentará executar o conteúdo dentro dos acentos graves como um comando do shell;

*Operadores lógicos

| Exemplo   | Nome | Resultado                                                |
|-----------|------|----------------------------------------------------------|
| $a and $b | E    | Verdadeiro (TRUE) se tanto $a quanto $b são verdadeiros. |
| $a or $b  | OU   | Verdadeiro se $a ou $b são verdadeiros.                  |
| $a xor $b | XOR  | Verdadeiro se $a ou $b são verdadeiros, mas não ambos.   |
| ! $a      | NÃO  | Verdadeiro se $a não é verdadeiro.                       |
| $a && $b  | E    | Verdadeiro se tanto $a quanto $b são verdadeiros.        |
| $a || $b  | OU   | Verdadeiro se $a ou $b são verdadeiros.                  |

* Operadores de array

| Exemplo   | Nome           | Resultado                                                                          |
|-----------|----------------|------------------------------------------------------------------------------------|
| $a + $b   | União          | União de $a e $b.                                                                  |
| $a == $b  | Igualdade      | TRUE se $a e $b tem os mesmos pares de chave/valor.                                |
| $a === $b | Identidade     | TRUE se $a e $b tem os mesmos pares de chave/valor na mesma ordem e do mesmo tipo. |
| $a != $b  | Desigualdade   | TRUE se $a não é igual a $b.                                                       |
| $a <> $b  | Desigualdade   | TRUE se $a não é igual a $b.                                                       |
| $a !== $b | Não identidade | TRUE se $a não é identico a $b.                                                    |

* Operador de tipo, é usado o comando *instanceof* para determinar se uma variável do PHP é uma instância de determinado objeto;
```php
if ($a instanceof mamiferos)
    //do something
```
